---
tags: [salesforce, admin, flow, assignment]
title: Assignment - Quick Reference
---

# Assignment

## 🎯 What is Assignment?

Assignment is used to modify **Variables** or **Collections** inside the Flow.

- It does **NOT** create records.
- It does **NOT** update Salesforce records.
- It only changes values stored **in memory**.

---

# ⚙️ Assignment Operators

Each line inside an Assignment element uses one of these operators:

| Operator | Effect |
|---|---|
| **Assign the value** (Set) | Overwrites the variable with a new value |
| **Add** | Adds a number/value to a numeric variable |
| **Subtract** | Subtracts a value from a numeric variable |
| **Add Item to Collection Variable** | Appends one record/value to a collection |
| **Remove Item from Collection Variable** | Removes matching item(s) from a collection |
| **Remove All from Collection Variable** | Empties the entire collection |
| **Remove First / Remove Position** | Removes a specific item by position |

> Multiple operations can be stacked in **one single Assignment element** — you don't need a separate element for each variable you touch.

---

# ✅ What Assignment Can Do

- Set Variable Value
- Change Variable Value
- Add Item to Collection
- Remove Item from Collection
- Clear Variable
- Build Data Before Create/Update

---

# Assignment vs Update Records

**Assignment**
```
Changes Variable
Only in Flow Memory
```
Example:
```
varCounter = 5
```

**Update Records**
```
Changes Salesforce Database
```
Example:
```
Account.Type = Customer
```

---

# Assignment vs Create Records

**Assignment**
```
Task Subject = "Call Customer"
```
Task still **DOES NOT exist**.

**Create Records**
Creates the actual Task in Salesforce.

---

# Variable Example

```
Variable:    varStatus
Assignment:  varStatus = "Approved"
Decision:    IF varStatus == "Approved"
```

---

# Counter Example

```
Initial:     Counter = 0
Assignment:  Counter = Counter + 1
Result:      Counter = 1
Again:       Counter = Counter + 1
Result:      Counter = 2
```

---

# Build Record Before Saving

```
Assignment: Task Subject = "Call Customer"
Assignment: Task OwnerId = Opportunity.OwnerId
Assignment: Task WhatId  = Opportunity.Id
```
Nothing is created yet.

```
Later → Create Records → Task is created.
```

---

# Collections

Assignment can:

| Action | Effect |
|---|---|
| **Add** | `Collection + Current Record` |
| **Remove** | `Collection - Current Record` |
| **Clear** | Empty Collection |

---

# 🔁 Assignment Inside a Loop (Bulkification Pattern)

The most common real-world use of Assignment is **building a collection inside a Loop**, so a single **Create Records** or **Update Records** element after the loop can process everything at once — instead of one DML operation per record.

```text
Loop over Get_Contacts
   ↓
Assignment: Add Item to Collection Variable
   (build a new Task record for each Contact,
    add it to colNewTasks)
   ↓
[Loop ends]
   ↓
Create Records (colNewTasks)   ← ONE Create Records call for all Tasks
```

> This is the correct way to avoid putting Create/Update Records *inside* the loop, which burns DML operations and risks hitting governor limits (see the Create Records and Get Records references).

---

# ⚠️ Important

Assignment:
- ❌ Does **NOT** create records.
- ❌ Does **NOT** update Salesforce.
- ❌ Does **NOT** query records.

It only changes values inside the **running Flow**.

---

# Memory vs Database

**Assignment**
```
RAM (Flow Memory) — Temporary
     ↓
Flow Ends
     ↓
Value disappears.
```

**Update Records**
```
Salesforce Database — Permanent.
```

---

# ✅ Best Practices

- Combine multiple variable changes into **one Assignment element** rather than several small ones — easier to read and maintain.
- Use Assignment + Collection **inside a loop**, then a single Create/Update Records **after** the loop, instead of DML inside the loop.
- Give variables descriptive names (`varApprovedCount`, not `var1`) so Assignment logic stays readable.

# ❌ Common Mistakes

- Expecting an Assignment on a record field (e.g., `$Record.Account.Type = "Customer"`) to save to Salesforce — it doesn't; you still need Update Records.
- Re-initializing a counter or collection variable *inside* a loop when it should be initialized **once before** the loop starts (this resets it every iteration instead of accumulating).
- Forgetting that Assignment values are lost the moment the Flow interview ends — nothing persists unless written out via Create/Update Records.

---

# 🗣️ Interview Summary

> Assignment modifies Variables or Collections.
> If I want to modify Salesforce data, I use **Update Records**.
> If I want to create Salesforce data, I use **Create Records**.
> If I only want to prepare or calculate data inside the Flow, I use **Assignment**.
