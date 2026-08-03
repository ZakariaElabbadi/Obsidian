---
tags:
  - automation
  - error-handling
  - integromat
title: Make.com Error Handling Guide
source: https://help.make.com/error-handling
---

# Make.com Error Handling Guide

> Verified against the official docs (help.make.com/error-handling) — corrections and additions from the source are marked ✅.

## 📑 Table of Contents
1. [[#1. Core Concept — What Is an Error Handler]]
2. [[#2. Types of Errors]]
3. [[#3. The 5 Error Handler Directives]]
4. [[#4. How the Error Handling Route Works]]
5. [[#5. Retry Mechanisms — Two Different Things]]
6. [[#6. Incomplete Executions Queue]]
7. [[#7. Scenario-Level Settings]]
8. [[#8. Alerting Strategy]]
9. [[#9. Advanced Patterns]]
10. [[#10. Common Pitfalls]]
11. [[#11. Error Code Reference]]
12. [[#12. Best Practices Checklist]]
13. [[#13. Resources]]

---

## 1. Core Concept — What Is an Error Handler

An **error handler** is a module attached to the end of an error-handling route. When the module it's attached to fails, the error handler **intercepts the failure** and tells the scenario what to do next — instead of the scenario just stopping.

**Without any error handler:** the scenario stops, and (if enabled) the failed run is pushed to the **Incomplete Executions** tab for you to fix manually.

**With an error handler:** the scenario follows whatever logic you defined — retry, skip, substitute a value, or cleanly stop — automatically, without you touching it.

> ✅ Official example: a form-to-CRM sync fails because a required "phone number" field is blank. Without a handler, the run stops and sits in Incomplete Executions until you manually type in a placeholder. With a **Resume** handler configured to substitute a default phone number, the scenario finishes on its own every time this happens.

---

## 2. Types of Errors

| Category | Examples | Recovers on retry? |
|---|---|---|
| **Connection (transient)** | Auth failures, timeouts, service unavailable | ✅ Yes |
| **Rate limiting (transient)** | Quota exceeded, too many requests, concurrency limits | ✅ Yes |
| **Data (structural)** | Invalid format, missing required field, type mismatch, validation failure | ❌ No |
| **Logic (structural)** | Infinite loops, bad mappings, router misconfiguration | ❌ No |
| **Module-specific** | e.g. Google Sheets "Row not found", Slack "Channel not found" | Depends |

> 🔑 **Key distinction:** Transient errors resolve themselves — retrying genuinely helps. Structural errors need a code/config fix — retrying just delays the inevitable and burns operations/quota.

---

## 3. The 5 Error Handler Directives

Every error-handling route must end in exactly one of these five. This is **not a HubSpot-style "pick a few options"** — Make defines precisely five, each with a fixed effect on scenario state ✅:

| Directive | Stops scenario? | Other bundles continue? | Final scenario status ✅ | Use case |
|---|---|---|---|---|
| **Skip** | No | Yes | **Success** | Occasional bad data that doesn't matter (nice-to-have lookup) |
| **Resume** | No | Yes | **Success** | Safe fallback value so the scenario can keep going |
| **Retry** | No (rest continues) | Yes | **Warning** | Isolated, record-level failures worth automatically retrying |
| **Commit** | Yes | No | **Warning** | Keep partial progress ("first 3 steps worked, keep them") |
| **Rollback** | Yes | No | **Error** | Undo transactional changes for consistency (default with no handler) |

### What each one actually does

- **Skip** — The failing module is treated as if it produced *no output*; the bundle is removed and the scenario moves to the next one. ⚠️ Danger: if a downstream module expects that output, you get silent data loss.
- **Resume** — Substitutes a predefined fallback value for the failed module's output and continues as if nothing happened. ⚠️ Danger: your data can quietly fill up with placeholder values for weeks before anyone notices.
- **Retry** — Removes the failing bundle from the flow, stores it as an **incomplete execution**, and retries it on your configured schedule while the rest of the bundles process normally. **Never use this for structural errors** — it just delays the failure and burns operations.
- **Commit** — Stops the run but **commits/keeps** all transactional changes made so far. Only meaningfully different from Rollback if you're using transactional (ACID-tagged) apps like Data Store or MySQL — otherwise it just stops the scenario.
- **Rollback** — Stops the run and **reverts** any changes in transaction-supporting modules only. This is the **default behavior** when no error handler is attached (and Incomplete Executions is off).

> ⚠️ Rollback **cannot** undo non-transactional actions — sent emails/Slack messages, deleted files, or already-fired HTTP/API calls (POST, DELETE, etc.). If your scenario is `CRM write → Sheet write → Slack notify` and the CRM step fails, Rollback won't "unsend" a Slack message that already went out. **Order your modules so non-transactional steps run last.**

---

## 4. How the Error Handling Route Works

```
Module → [Error] → (transparent dotted connection) → Error-handling route → Directive
```

- Add one by right-clicking any module → **"Add error handler."**
- The route is visually a **transparent, dotted line** from the module.
- **Doesn't have to contain an error-handler module at all** — it can be just a Slack/Email notification, with no directive module attached.
- **Doesn't consume operations** — running the error route is free.
- **If nothing in the error route itself errors** → Make treats it as skipped, and the run is marked **successful**.
- **If a module inside the error route also errors** → the run ends with an **error** status (this is how "nested" error handling behaves).

---

## 5. Retry Mechanisms — Two Different Things

Make has two mechanisms people often conflate:

| Mechanism | Triggered by | Schedule | Requires |
|---|---|---|---|
| **Automatic retry (built into Make)** | Connection errors, rate limits, timeouts | Exponential backoff: ~1m, 10m, 10m, 30m… up to 8 attempts | **Store incomplete executions** = ON |
| **Retry directive (your handler)** | Any error you route into it | Your custom attempts × interval | Configured per-module, independent of the scenario setting |

> ⚠️ Automatic retries **only** fire for transient errors. Structural errors (HTTP 400, 401, mapping failures) never auto-retry — they just fail and (if enabled) land in Incomplete Executions.

---

## 6. Incomplete Executions Queue

When a **Retry directive fires**, or a module fails with **no handler attached**, Make can store the run's exact data + failure state as an **incomplete execution** for later manual or automatic resume.

### Requirements
- **"Store incomplete executions" must be ON** in Scenario Settings (**OFF by default**).
- A failure on the **first module** of a scenario is only captured if that first module has a **Retry handler directly attached to it** ✅ — otherwise it's lost with no queue entry.

### Router behavior (official)
When Incomplete Executions is ON and a bundle errors inside one branch of a **Router**:
- The scenario **does not stop** — the error is treated as a warning.
- The bundle stops **only within that failing route**.
- The **same bundle still completes normally through every other matching route.**
- The failed portion is stored in the Incomplete Executions tab.

→ A single bundle can partially succeed: finishing in some branches while being captured as "incomplete" in just the one that failed.

### Operational reality
- A queue of 5 = a five-minute fix.
- A queue of 200 discovered three weeks later = a reconciliation nightmare (source data has since changed, manual edits conflict).
- **Fix:** review the queue on a schedule shorter than the rate at which failures accumulate.

### Limits
- Resolved executions auto-delete after **30 days**.
- There's an org-wide storage cap (usage-based) — once hit, new incomplete executions are blocked (see **Enable data loss** setting below).

---

## 7. Scenario-Level Settings

Found under **Scenario Settings → (Advanced)**:

| Setting | Default | Effect |
|---|---|---|
| **Store incomplete executions** | OFF | Required for auto-retries and the Incomplete Executions queue to work at all |
| **Sequential processing** | OFF | Postpones the next run until the previous one finishes *and* all incomplete executions are resolved. Critical for webhook-triggered scenarios, which otherwise run in parallel and can finish out of order |
| **Enable data loss** | — | When incomplete-execution storage is full: **ON** = discard the data and keep running on schedule; **OFF** = disable scheduling instead |
| **Number of consecutive errors** | 3 | Auto-disables the scenario after this many failed runs in a row. **Exception:** instant (webhook) triggers disable *immediately* on error, and also immediately on `AccountValidationError`, `OperationsLimitExceededError`, or `DataSizeLimitExceededError` regardless of the counter |
| **Auto commit** | OFF (commit at end) | ON = commit transactional (ACID-tagged) module changes right after each one happens, rather than only after the whole run succeeds |
| **Commit trigger last** | OFF (commit in order) | ON = commit the *first* module's transactional changes *last* instead of in execution order |
| **A run that ends with a Warning** | — | Scheduling continues normally — only an **Error** status affects the consecutive-error counter |

---

## 8. Alerting Strategy

**Golden rule: alert on the *directive*, not on every error.**

| Directive / event | Alert? | Why |
|---|---|---|
| Skip / Resume (safe fallback) | ❌ No | System is working exactly as designed |
| Retry (transient) | ❌ No | Auto-resolves |
| **Commit / Rollback / Break** | ✅ Yes | The system couldn't safely decide on its own |
| **Incomplete execution created** | ✅ Yes | Needs a human |

**Implementation tips:**
- Route Commit/Rollback failures → Slack/Email/Webhook.
- Time-critical processes (payments, contracts) → webhook into your **existing** paging system (PagerDuty, Opsgenie) — don't build a parallel alerting channel.
- Avoid "notify on every single error" — this leads to alert fatigue and the channel gets muted within a week.

---

## 9. Advanced Patterns

### Circuit Breaker
```
Counter module → increments on each error
  → if > 5 errors in 10 min → pause scenario → alert team
```

### Dead Letter Queue
```
Failed bundle → store in Data Store / Sheet
  → manual review process
  → "Replay" button (HTTP trigger re-injects it)
```

### Graceful Degradation
```
Primary API → [Error] → Fallback API → Cached/static data → Hardcoded default
```

### Router-based error triage (route by error code)
```
[HTTP: Get User]
   ├── Success → [Process User]
   └── Error → [Router: branch on {{error.code}}]
                  ├── 401 → refresh token → Resume
                  ├── 429 → sleep 60s → Resume
                  ├── 404 → create user → Resume
                  └── other → alert team → log bundle → Rollback
```

---

## 10. Common Pitfalls

| Pitfall | Symptom | Fix |
|---|---|---|
| No handler on a "safe" module | Silent halt discovered months later | Give **every** module an explicit directive |
| Resume-with-fallback everywhere | CRM slowly fills with placeholder data | Only use Resume where the fallback is genuinely safe |
| High retry counts on structural errors | Ops quota burned, real bug hidden | Zero/low retries on mapping and auth errors |
| Incomplete Executions ON but never checked | 200+ item backlog, unreconcilable | Review the queue on a schedule shorter than the failure rate |
| Alerting on every error | Team mutes the Slack channel | Alert only on Commit/Rollback/Incomplete execution |
| Expecting Rollback to "unsend" an email | Email/Slack message sent despite a later DB failure | Put non-transactional steps **last** in module order |
| First module fails with no Retry handler | Data lost, nothing in the queue | Attach a Retry handler directly to the first module |

---

## 11. Error Code Reference

### HTTP modules
| Code | Meaning | Action |
|---|---|---|
| 400 | Bad Request | Check mapping/validation |
| 401 | Unauthorized | Refresh token/credentials |
| 403 | Forbidden | Check permissions/scopes |
| 404 | Not Found | Verify resource IDs |
| 429 | Rate Limited | Add delay/retry |
| 500 | Server Error | Retry with backoff |
| 503 | Unavailable | Circuit breaker |

### Database modules
| Code | Meaning |
|---|---|
| ER_DUP_ENTRY | Duplicate key |
| ER_NO_REFERENCED_ROW | Foreign key violation |
| ER_DATA_TOO_LONG | Field length exceeded |

### Available error variables (inside a handler)
`{{error.message}}` · `{{error.type}}` · `{{error.code}}` · `{{error.module}}` · `{{error.bundle}}` · `{{error.scenario}}` · `{{error.execution}}`

---

## 12. Best Practices Checklist

- [ ] Attach an error handler to every **critical** module (payments, DB writes, external API calls, email/SMS).
- [ ] Name error handlers descriptively (`"Error: Payment Gateway Timeout - Notify Finance"`, not `"Error Handler 1"`).
- [ ] Log structured error data (timestamp, scenario, module, message, bundle, execution ID) somewhere queryable.
- [ ] Test with **Run once** + intentionally invalid data; simulate downtime/rate limiting.
- [ ] Turn on **Store incomplete executions** for any scenario handling important data.
- [ ] Order modules so non-transactional actions (sending, deleting) happen **last**.
- [ ] Reserve aggressive Retry configs for genuinely flaky external APIs — not structural bugs.
- [ ] Review the Incomplete Executions queue on a fixed schedule.
- [ ] Use the **Throw** tool to deliberately test your error-handling routes (it also lets you enforce custom business-rule validation with a custom message/code).

---

## 13. Resources

- [Error handling (index)](https://help.make.com/error-handling)
- [Introduction to errors and warnings](https://help.make.com/introduction-to-errors-and-warnings)
- [Overview of error handling](https://help.make.com/overview-of-error-handling)
- [Error handlers](https://help.make.com/error-handlers)
- [Exponential backoff](https://help.make.com/exponential-backoff)
- [Throw](https://help.make.com/throw)
- [Common errors and warnings and their fixes](https://help.make.com/common-errors-and-warnings-and-their-fixes)
- [Scenario settings](https://help.make.com/evar6qlowv4yyuneyv00)
