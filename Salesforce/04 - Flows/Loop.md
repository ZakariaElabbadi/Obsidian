---
tags: [salesforce, admin, flow, loop]
title: Loop - Quick Reference
---

# Loop

## 🎯 What is a Loop?

A **Loop** is used to iterate through a **Record Collection**, processing **one record at a time**.

You use a Loop when you need to perform actions for each record in a collection.

---

# 📌 When to Use a Loop?

Use a Loop when you have:
- Multiple Contacts
- Multiple Opportunities
- Multiple Cases
- Multiple Tasks

...and you need to process each record individually.

> A Loop doesn't have to come right after a **Get Records** — it can iterate over **any Collection Variable**, including one you built manually with Assignment.

---

# 🧱 Loop Structure

```text
Get Records (All Records)
     ↓
   Loop
     ↓
Current Item
     ↓
Decision / Assignment / Create / Update
     ↓
Next Item
     ↓
    ...
     ↓
After Last Item
     ↓
   End
```

---

# Current Item

During each iteration, the Loop exposes one record called the **Current Item**.

**Example:**
```text
Contacts: Ahmed, Ali, Sara
```
```text
Iteration 1 → Loop_Contact = Ahmed
Iteration 2 → Loop_Contact = Ali
Iteration 3 → Loop_Contact = Sara
```

> ⚠️ **Scope:** The Current Item variable only holds a valid value **while inside the Loop**. Referencing it *after* the Loop (outside/after "After Last Item") is meaningless — it will hold whatever the *last* iteration left it as, which is rarely what you want. If you need data from every iteration, add it to a **Collection Variable** instead.

---

# After Last Item

Runs **only once**, after the Loop finishes all iterations.

**Example:**
```text
Loop
  ↓
Create Tasks
  ↓
After Last Item
  ↓
Send Email
```
Only **one** email is sent — not one per Contact.

> If the collection being looped over is **empty**, the Loop skips straight to **After Last Item** with zero iterations — it never errors.

---

# Assignment Inside Loop

Use Assignment to modify the Current Item.

```text
Loop_Contact.Department = "Sales"
```

---

# Record Collection Variable

A Record Collection Variable stores multiple records.

```text
Name:   varUpdatedContacts
Object: Contact
Type:   Record Collection
```

---

# ✅ Bulk Update Pattern

**Correct:**
```text
Get Records
   ↓
 Loop
   ↓
Assignment
   ↓
Add Current Item to Collection
   ↓
After Last Item
   ↓
Update Records   ← ONE bulk DML call
```

**Avoid:**
```text
Loop
   ↓
Update Records   ← DML runs once PER record — burns limits
```

---

# Add Current Record to Collection

**Correct:**
```text
varUpdatedContacts
   Add
Loop_Contact
```

**Wrong:**
```text
Loop_Contact
   Add
varUpdatedContacts
```

**Reason:**
- A Collection can contain Records.
- A Record cannot contain a Collection.

---

# Loop + Decision

```text
Loop
  ↓
Decision: Department = Sales
  ↓ Yes              ↓ No
Create Task        Skip
```

---

# Loop + Create Records

```text
Loop
  ↓
Create Task
  Subject = Welcome Call
  OwnerId = Loop_Contact.OwnerId
  WhoId   = Loop_Contact.Id
```

> Same bulk-update principle applies here — prefer building a Task **Collection** inside the loop and calling **Create Records once** after it, rather than creating one Task per iteration.

---

# Loop + Update Records

**Best Practice:**
```text
Loop
  ↓
Assignment
  ↓
Add to Collection
  ↓
After Last Item
  ↓
Update Records
```

---

# Loop + Get Records

**Common Example:**
```text
Start
  ↓
Get Contacts
  ↓
Loop
  ↓
Create Task
```

---

# 🔂 Nested Loops (Use With Caution)

You *can* put a Loop inside another Loop (e.g., loop Accounts, and for each Account loop its Contacts), but:

- **Never call Get Records inside a loop** to fetch the inner collection — query everything once beforehand and loop over the pre-fetched data in memory.
- Nested loops multiply iterations (`Accounts × Contacts per Account`) — with large data volumes this can get slow or hit Apex CPU time limits.
- Each nested Loop needs its **own** Current Item variable — don't reuse the outer loop's variable name.

---

# ⚡ Alternative: Collection Filter (No Loop Needed)

If all you need is to **filter** a collection (e.g., "only Contacts with Department = Sales") and you're **not** performing an action per record, use the **Collection Filter** element instead of a Loop + Decision + Add-to-Collection. It's simpler and avoids unnecessary iteration logic when filtering is the only goal.

---

# ✅ Best Practices

- Loop only over Record Collections.
- Use Current Item inside the Loop only — never reference it after the loop ends.
- Use After Last Item for one-time, post-loop actions (send one summary email, one Create/Update Records call).
- Use Assignment to modify records, then add them to a Collection.
- Call Create/Update Records **once, after** the Loop — never inside it.
- Never call Get Records inside a Loop (see the Get Records reference).
- For simple filtering with no per-record action, use **Collection Filter** instead of a Loop.

# ❌ Common Mistakes

- Update Records inside Loop.
- Creating unnecessary Get Records (query once, loop in memory).
- Confusing a Record with a Collection (see "Add Current Record to Collection" above).
- Using "All Records" in Get Records when you only need one (by unique Id).
- Mixing up OwnerId, WhoId, and WhatId when creating Tasks in a loop.
- Nesting a Get Records call inside a nested loop instead of querying once upfront.
- Referencing the Current Item variable after the Loop has ended.

---

# 🧠 Golden Rules

- A Loop works on **one record at a time**.
- Current Item changes **every** iteration — and is only valid inside the loop.
- A Collection stores **multiple** records.
- After Last Item executes **only once**.

**Always think:**
```
Collection → Loop → Current Item → Assignment → Collection → Update
```
