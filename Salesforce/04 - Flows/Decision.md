---
tags: [salesforce, admin, flow, decision]
title: Decision - Quick Reference
---

# Decision

## 🎯 Purpose
A Decision element works like an **if / else** statement.
It evaluates one or more conditions and sends the Flow through the matching path.

---

# 🔀 Syntax

```text
IF condition A
    → Path A
ELSE IF condition B
    → Path B
ELSE
    → Default Outcome
```

---

# 🧪 Example

```text
Stage = Prospecting
    → Create Task

Stage = Qualification
    → Create Different Task

Otherwise
    → End Flow
```

---

# 🧩 Components

- **Outcome** — a named path with its own condition(s)
- **Condition** — the logic tested (field, operator, value)
- **Default Outcome** — runs only if no other Outcome matches

---

# ⚙️ Combining Multiple Conditions (AND / OR)

An Outcome can have **more than one condition**. You choose how they combine:

| Logic | Behavior |
|---|---|
| **All Conditions Are Met (AND)** | Every condition must be true |
| **Any Condition Is Met (OR)** | At least one condition must be true |
| **Custom Logic** | Write your own formula, e.g. `(1 AND 2) OR 3` |

**Example:**
```text
Outcome: High Value Enterprise Deal
Condition 1: Amount > 50000
Condition 2: Type = "New Business"
Logic: 1 AND 2
```

---

# 🔢 Common Operators

- Equals
- Not Equals
- Greater Than / Greater Than or Equal
- Less Than / Less Than or Equal
- Is Null
- Contains / Starts With (text fields)

---

# ⚠️ Order Matters

> Outcomes are evaluated **top to bottom**, and the **first match wins** — later matching outcomes are skipped.

**✅ Correct (most restrictive first):**
```text
Amount >= 50000   → Outcome A
Amount >= 10000   → Outcome B
Default
```

**❌ Incorrect:**
```text
Amount >= 10000   → Outcome A
Amount >= 50000   → Outcome B   ← never runs, already caught by Outcome A
Default
```

---

# 💡 Tips

- Outcomes are checked from top to bottom.
- The first matching outcome is executed.
- Always keep a **Default Outcome** — never assume one of your conditions will always be true.
- Give each Outcome a clear, descriptive name (not "Outcome 1", "Outcome 2").

---

# ✅ Best Practices

- Order outcomes from **most restrictive to least restrictive**.
- Use **AND/OR logic** instead of creating many near-duplicate Decision elements.
- Add a **Null check** as its own condition/outcome if a field might be empty — comparing against a null field can behave unexpectedly.
- Keep condition logic readable; if it gets too complex, consider a Formula resource instead.

---

# ❌ Common Mistakes

- Placing a broader condition **before** a narrower one, so the narrower one never triggers.
- Forgetting the **Default Outcome**, causing the Flow to silently do nothing when no condition matches.
- Not accounting for **null/blank values** in a condition (e.g., `Amount > 10000` when Amount is empty).
- Using several separate Decision elements when one Decision with AND/OR logic would be simpler and clearer.
