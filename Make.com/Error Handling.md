# Make.com Error Handling Guide

## Overview

Make.com (formerly Integromat) provides robust error handling mechanisms to manage failures in automation scenarios. Understanding these mechanisms is crucial for building reliable workflows.

---

## Types of Errors in Make.com

### 1. **Connection Errors** (Transient)
- API authentication failures
- Network timeouts
- Service unavailable
- Invalid credentials

### 2. **Data Errors** (Structural)
- Invalid data format
- Missing required fields
- Data type mismatches
- Validation failures

### 3. **Logic Errors** (Structural)
- Infinite loops
- Incorrect mappings
- Conditional logic failures
- Router misconfiguration

### 4. **Rate Limiting Errors** (Transient)
- API quota exceeded
- Too many requests
- Concurrent execution limits

### 5. **Module-Specific Errors**
- Each app/module has unique error codes
- Example: Google Sheets "Row not found", Slack "Channel not found"

> **Key Distinction**: **Transient errors** (connection, rate limits) recover on their own — retry works. **Structural errors** (bad mappings, expired tokens, malformed data) require code/config fix — retry just delays failure.

---

## The 5 Error Handler Directives (Core Concept)

When you add an error handler route to a module, it **must end in exactly one of five directives**. Each fundamentally changes scenario state:

| Directive | Stops Run? | Continues Other Bundles? | Keeps Prior Changes? | Use Case |
|-----------|------------|--------------------------|---------------------|----------|
| **Skip** | No | Yes | N/A | Optional enrichment (lookup that's nice-to-have) |
| **Resume** | No | Yes | N/A | Safe fallback value (continue with default) |
| **Retry** | No (rest continues) | Yes | N/A | Isolated record-level failures |
| **Commit** | Yes | No | **Yes** | Partial progress worth keeping |
| **Rollback** | Yes | No | **Yes*** | Transactional consistency (DB/Data Store only) |

> *Rollback only reverts modules supporting transactions (database, data store). Cannot undo sent emails, deleted files, or API calls already made.

### Directive Behavior Details

**Skip** — Treats module as producing no output. Downstream modules map against empty values. **Danger**: Silent data loss if downstream expects the output.

**Resume** — Supplies fallback value, continues as if module succeeded. **Danger**: Scenario runs on placeholder data unnoticed for weeks.

**Retry** — Parks failing bundle, retries on your schedule (attempts × interval), other bundles process normally. **Not for structural errors**.

**Commit** — Stops scenario, marks run successful, keeps all prior transactional changes. Use when "first 3 steps succeeded, keep them even if step 4 fails."

**Rollback** — Stops scenario, reverts transactional changes in *this execution only*. Default behavior when **no error handler attached**. Use for multi-step writes that must stay consistent.

---

## Error Handling Mechanisms

### 1. **Error Handler Route (Built-in)**
```
Module → [Error] → Error Handler Module → [Directive]
```
- Right-click any module → "Add error handler"
- Creates alternative execution path on failure
- **Must end in one of 5 directives above**

> **Key Properties (Official Docs)**:
> - **Error handler routes don't consume operations** — free to execute
> - **Route doesn't require an error handler module** — can be just Slack/Email notification
> - **If no module in error route outputs error** → Make skips the error (run succeeds)
> - **If module in error route outputs error** → run ends with error (nested error handling)
> - Visual: transparent dotted connection from module

### 2. **Two Retry Mechanisms (Different!)**

| Mechanism | Trigger | Schedule | Config |
|-----------|---------|----------|--------|
| **Automatic (Make)** | Connection errors, rate limits, timeouts | Exponential backoff: ~1m, 10m, 10m, 30m... up to 8 attempts | **Requires** "Store incomplete executions" ON in scenario settings |
| **Handler (Retry directive)** | Any error you configure | Your custom attempts × interval | Per-module, independent of scenario setting |

> **Critical**: Automatic retries only fire for transient errors. Structural errors (400, 401, mapping failures) never auto-retry.

### 3. **Ignore Errors** (Module Setting)
- Toggle "Ignore errors" on module
- Continues execution despite failure
- **No directive**, no error handler route created
- Use with extreme caution — hides issues completely

### 4. **Break / No Handler** (Default = Rollback)
- No error handler attached → **Rollback behavior**
- Stops scenario, reverts transactional changes
- Marks run as failed

---

## Incomplete Executions Queue

When a **Retry directive fires** or **module fails with no handler**, Make can store the run — exact data + state at failure point — as an **incomplete execution** for later manual/auto resume.

### Requirements
- **"Store incomplete executions" MUST be ON** in Scenario Settings (OFF by default)
- First-module failures only stored if **Retry handler attached directly to that module**

### Router Module Behavior (Official)
When "Store incomplete executions" is enabled and a bundle errors inside one of a **Router's routes**:
- Scenario **does not stop** — error treated as warning
- Bundle stops at failing module **within that route only**
- **Same bundle continues through ALL other routes** whose filters match
- Errored execution stored in incomplete executions tab

> A single bundle can partially succeed — completing in some routes while captured as incomplete in the failed route.

### Operational Reality
- Queue of 5 = 5-min fix
- Queue of 200 discovered 3 weeks late = reconciliation nightmare (data changed elsewhere, manual edits conflict)
- **Fix**: Check queue on schedule short enough it never grows large

### Limits
- Resolved executions auto-deleted after **30 days**
- Org-wide storage cap (usage-based) — new incomplete executions blocked when hit

---

## Alerting That Actually Gets Checked

**Golden Rule**: Alert on the **directive**, not on the error.

| Module Directive | Alert? | Why |
|------------------|--------|-----|
| Skip / Resume (with safe fallback) | **No** | System working as designed |
| Retry (transient) | **No** | Auto-resolves |
| **Commit / Rollback / Break** | **YES** | System couldn't decide safely |
| **Incomplete execution created** | **YES** | Human intervention needed |

### Implementation
- Route Break/Commit/Rollback → Slack/Email/Webhook
- Time-critical (payments, contracts) → Webhook → **existing paging/ticketing system** (PagerDuty, Opsgenie)
- Avoid: "Notify on every error" → alert fatigue → ignored within a week

---

## Error Handler Modules

### **Router (Error Handling)**
```
Error → Router → Route 1: Notify Admin
              → Route 2: Log to Database
              → Route 3: Retry with Modified Data
              → Route 4: Create Ticket
```

### **Set Variable**
Store error details for later use:
- `{{error.message}}`
- `{{error.type}}`
- `{{error.module}}`

### **HTTP / Webhook**
Send error to external monitoring:
- Slack, Discord, Email
- PagerDuty, Opsgenie
- Custom logging endpoint

### **Sleep + Resume**
Implement custom retry logic:
```
Error → Sleep (300s) → Resume from Failed Module
```

### **Throw (Tool)**
- **Force an error** intentionally in a scenario
- Use for: validation checks, business rule enforcement, testing error handlers
- Can specify custom error message, type, code
- Triggers error handler route like any other error

---

## Critical: Transient vs Structural Errors

| Error Type | Examples | Retry Works? | Correct Handling |
|------------|----------|--------------|------------------|
| **Transient** | Timeout, 429 rate limit, 503, network blip | **Yes** | Retry directive / Auto-retry |
| **Structural** | 400 bad request, 401 expired token, mapping error, malformed JSON, missing field | **No** | Fix code/config, alert human |

> **Anti-pattern**: High retry counts on structural errors = burns ops quota, delays detection, adds log noise. Reserve aggressive retries for flaky external APIs only.

---

## Rollback Limitations (Important)

Rollback **only** reverts:
- Database modules (MySQL, PostgreSQL, SQL Server, etc.)
- Data Store modules
- Other transaction-supporting modules

Rollback **CANNOT** undo:
- Sent emails / Slack messages / SMS
- Deleted files
- HTTP API calls already executed (POST, DELETE, etc.)
- Any non-transactional module action

> If your scenario: CRM write → Spreadsheet write → Slack notify, and CRM fails — Rollback won't "unsend" the Slack if it already fired. Order modules so non-transactional steps come LAST, or use Commit + manual cleanup.

---

## Advanced Patterns

### **Circuit Breaker Pattern**
```
Counter Module → Increment on Error
                → If > 5 errors in 10min → Pause Scenario
                → Alert Team
```

### **Dead Letter Queue**
```
Failed Data → Store in Data Store / Google Sheets
              → Manual Review Process
              → Replay Button (HTTP trigger)
```

### **Graceful Degradation**
```
Primary API → [Error] → Fallback API
                       → Cache/Static Data
                       → Default Values
```

---

## Error Data Structure

When error handler triggers, these variables available:

| Variable              | Description                                           |
| --------------------- | ----------------------------------------------------- |
| `{{error.message}}`   | Human-readable error message                          |
| `{{error.type}}`      | Error category (e.g., `DataError`, `ConnectionError`) |
| `{{error.code}}`      | Module-specific error code                            |
| `{{error.module}}`    | Name of failed module                                 |
| `{{error.bundle}}`    | Input bundle that caused error                        |
| `{{error.scenario}}`  | Scenario ID                                           |
| `{{error.execution}}` | Execution ID                                          |

---

## Best Practices

### 1. **Always Add Error Handlers to Critical Modules**
- Payment processing
- Database writes
- External API calls
- Email/SMS sending

### 2. **Use Descriptive Error Handler Names**
```
✅ "Error: Payment Gateway Timeout - Notify Finance"
❌ "Error Handler 1"
```

### 3. **Implement Structured Logging**
```json
{
  "timestamp": "{{now}}",
  "scenario": "{{scenario.name}}",
  "module": "{{error.module}}",
  "error": "{{error.message}}",
  "bundle": "{{error.bundle}}",
  "executionId": "{{execution.id}}"
}
```

### 4. **Test Error Scenarios**
- Use "Run once" with invalid data
- Simulate API downtime
- Test rate limiting

### 5. **Monitor Scenario Health**
- Enable "Send email on error" in scenario settings
- Use Make's built-in dashboard
- Integrate with external monitoring

---

## Official Decision Framework: When to Use Error Handlers

Per Make.com docs — most frequent errors (RateLimitError, ConnectionError) are handled by default **if incomplete executions enabled**. Custom error handlers needed when:

| Question | Decision |
|----------|----------|
| **How important is the data?** | Critical → Store incomplete executions; resolve manually or bulk retry |
| **What error type & frequency?** | Rare + transient (RateLimitError) → Default handling. Critical (InvalidAccessTokenError, InconsistencyError) → Custom handler |
| **Impact of error?** | No impact → Skip handler. High impact → Incomplete executions + alert |

### Default Handling for Common Errors
- **RateLimitError / ConnectionError**: Auto-retries with exponential backoff (requires incomplete executions ON)
- **Other errors**: Rollback (default) or incomplete execution stored

---

## Scenario-Level Error Settings

### **Scenario Settings → Error Handling**
- **Max consecutive errors**: Auto-disable after N failures (default: 3). **Exception**: Instant triggers (webhooks) disable immediately on error.
- **Immediate disable on**: `AccountValidationError`, `OperationsLimitExceededError`, `DataSizeLimitExceededError`
- **Error notification email**: Recipients for failure alerts
- **Store incomplete executions**: **ON** (required for auto-retries & queue) — OFF by default
- **Process data in order**: Postpones next run until previous finishes + all incomplete executions resolved. Critical for webhooks & scenarios with incomplete executions.
- **Enable data loss**: When storage full — ON = discard data & continue; OFF = disable scenario scheduling
- **Auto commit**: ON = commit transactional changes after each module; OFF = commit at end (default). Affects only "ACID" tagged modules (Data Store, MySQL, etc.)
- **Commit trigger last**: ON = commit first module's changes last; OFF = commit in execution order. Affects only transactional modules.

### **Scheduling & Errors**
- Failed scheduled runs don't block next run
- Use "Run scenario" module for dependency chains
- Warnings don't disable scheduling; errors do (after consecutive threshold)

---

## Common Pitfalls (From Production)

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| No handler on "safe" module | Silent halt months later | Map **every** module to a directive |
| Resume with fallback everywhere | CRM full of placeholder data | Only Resume where fallback is truly safe |
| High retries on structural errors | Ops quota burned, real issue hidden | Low/no retries on mapping/auth errors |
| Incomplete executions ON, never checked | 200+ queue, unreconcilable backlog | Schedule queue review < frequency of failures |
| Alert on every error | Team ignores Slack channel | Alert only on Break/Commit/Rollback/Incomplete |
| Rollback expected to undo email | Email sent despite DB failure | Put non-transactional steps LAST |
| First module fails, no queue entry | Lost data, no retry | Add Retry handler to first module |

---

## Common Error Codes Reference

### **HTTP Modules**
| Code | Meaning | Action |
|------|---------|--------|
| 400 | Bad Request | Check mapping/validation |
| 401 | Unauthorized | Refresh token/credentials |
| 403 | Forbidden | Check permissions/scopes |
| 404 | Not Found | Verify resource IDs |
| 429 | Rate Limited | Add delay/retry |
| 500 | Server Error | Retry with backoff |
| 503 | Unavailable | Circuit breaker |

### **Database Modules**
| Code | Meaning |
|------|---------|
| ER_DUP_ENTRY | Duplicate key |
| ER_NO_REFERENCED_ROW | Foreign key violation |
| ER_DATA_TOO_LONG | Field length exceeded |

---

## Debugging Tips

1. **Use "Run once" with test data**
2. **Check execution inspector** (bubble icon)
3. **Enable "Show all bundles"** in module output
4. **Use Set Variable to capture intermediate state**
5. **Test error handlers independently**

---

## Example: Complete Error Handling Flow

```
[HTTP: Get User] 
    │
    ├── Success → [Process User]
    │
    └── Error → [Router: Check error.code]
                    │
                    ├── 401 → [Refresh Token] → [Resume: Get User]  (Directive: Resume)
                    │
                    ├── 429 → [Sleep 60s] → [Resume: Get User]       (Directive: Resume)
                    │
                    ├── 404 → [Create User] → [Resume: Get User]     (Directive: Resume)
                    │
                    └── Other → [Slack: Alert Team] 
                                  → [Data Store: Log Failed Bundle]
                                  → [Break]                          (Directive: Rollback)
```

> Use **Router** on error handler to route by `{{error.code}}` or `{{error.type}}` to different directives.

---

## Resources

- [Make Error Handling Docs](https://www.make.com/en/help/error-handling)
- [Error Types Reference](https://www.make.com/en/help/error-types)
- [Rollback Error Handler Docs](https://help.make.com/rollback-error-handler)
- [Exponential Backoff Docs](https://help.make.com/exponential-backoff)
- [Incomplete Executions Docs](https://help.make.com/incomplete-executions)
- [Overview of Error Handling (Official)](https://help.make.com/overview-of-error-handling)
- [Error Handlers Reference](https://help.make.com/error-handlers)
- [Throw Tool Docs](https://help.make.com/throw)
- [Common Errors & Fixes](https://help.make.com/common-errors-and-warnings-and-their-fixes)
- [Scenario Settings Docs](https://help.make.com/evar6qlowv4yyuneyv00)
- [Alltomate Deep Dive](https://alltomate.com/blogs/make-com-error-handling/) — Source for directive behavior & operational patterns
- [Community Templates](https://www.make.com/en/templates) — Search "error handling"
- [Make Academy](https://www.make.com/en/academy) — Error Handling Course

---

*Last Updated: {{date}}*
*Version: 2.1 — Added official docs insights: route properties, router behavior, decision framework, scenario settings details, Throw tool*