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

- **Outcome**
- **Condition**
- **Default Outcome**

---

# 💡 Tips

- Outcomes are checked **from top to bottom**.
- The **first matching** outcome is executed.
- Always keep a **Default Outcome**.
