---
tags: [salesforce, admin, flow, decision, lesson04]
title: Lesson 04 - Decision Element
---

# Lesson 04 - Decision Element

## 🎯 Objective
Learn how to make decisions in Flow.

---

# 🔀 Decision = IF / ELSE IF / ELSE

**Programming:**
```text
if (...)
else if (...)
else
```

**Flow:**
- Outcome 1
- Outcome 2
- Default Outcome

---

# ⚙️ Common Operators

- Equals
- Not Equals
- Greater Than
- Greater Than or Equal
- Less Than
- Less Than or Equal
- Is Null

---

# ⚠️ Important Rule

> Decision outcomes are evaluated **from top to bottom**.
> Always put the **most restrictive** condition first.

**✅ Correct:**
```text
Amount >= 50000
     ↓
Amount >= 10000
     ↓
Default
```

**❌ Incorrect:**
```text
Amount >= 10000
     ↓
Amount >= 50000
```
> The second outcome will **never execute**.

---

# ✅ Best Practices

- Give meaningful Outcome names.
- Use **Default Outcome** for all remaining cases.
- Keep Decision logic simple.
