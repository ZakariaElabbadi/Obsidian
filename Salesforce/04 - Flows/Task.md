---
tags: [salesforce, admin, task, whoid, whatid]
title: Task - Quick Reference
---

# Task

## 🎯 Purpose
A Task represents an activity that someone needs to complete.

**Examples:**
- Call customer
- Send email
- Follow up
- Schedule meeting

---

# 🧩 Important Fields

## Subject
The title of the task.

**Example:**
```
Call New Lead
```

---

## Assigned To (OwnerId)
The user responsible for completing the task.

Usually:
```
Triggering Record → OwnerId
```

---

## Status
**Examples:**
- Not Started
- In Progress
- Completed
- Waiting on someone else
- Deferred

> The `IsClosed` field is `true` automatically once Status is a "closed" value (e.g. Completed).

---

## Priority
**Examples:**
- High
- Normal
- Low

---

## Due Date (ActivityDate)
The date the task should be completed by.

**Example:**
```
ActivityDate = TODAY() + 3
```
Used often in Flow to schedule follow-ups a few days after a trigger event.

---

## Description
A free-text field for extra details or notes about the task — useful for context when the Subject alone isn't enough.

---

## Type / TaskSubtype
Categorizes the kind of activity.

**Examples:**
- Call
- Email
- Task (general)

Useful for reporting (e.g., counting how many "Calls" a rep logged this week).

---

# 🔗 Linking a Task

A Task can be related to other records in **two independent ways** — they are not mutually exclusive.

## WhoId (Name ID)
Used for **PEOPLE**.

**Supported:**
- Lead
- Contact

**Examples:**
- ✓ Call Lead
- ✓ Email Contact

---

## WhatId (Related To ID)
Used for **BUSINESS RECORDS**.

**Supported:**
- Account
- Opportunity
- Case
- Campaign
- Contract
- Custom Objects

**Examples:**
- ✓ Follow up Opportunity
- ✓ Review Case
- ✓ Meeting for Account

---

# ⚠️ Rules

1. **WhoId only accepts People** (Lead or Contact). **WhatId only accepts Business Records.** Putting a Lead ID into WhatId (or an Opportunity ID into WhoId) throws `FIELD_INTEGRITY_EXCEPTION`.
2. **WhoId and WhatId CAN be used together on the same Task** — this is a common and valid pattern.
   Example: `WhoId = Contact` + `WhatId = Opportunity` → "Follow up with Ahmed about the CRM License deal."
3. **A Lead can never appear in WhatId.** If the Task relates to a Lead, only WhoId is used (no WhatId at all).

| Record | Field |
|---|---|
| Lead | WhoId only |
| Contact | WhoId |
| Opportunity | WhatId |
| Account | WhatId |
| Case | WhatId |

---

# 🧠 Visual Memory

```
Person          → WhoId
Business Record → WhatId
```

---

# ✅ Best Practices

- Always set a meaningful **Subject** — avoid generic ones like "Task" or "Follow up".
- Set a **Due Date (ActivityDate)** so the task shows up correctly in the user's task list/calendar.
- When relating a Task to both a person and a record, double-check WhoId/WhatId map to the correct object type.
- Use **Type/TaskSubtype** consistently to make reporting on activities meaningful.

# ❌ Common Mistakes

- Putting a Lead ID into `WhatId` → causes `FIELD_INTEGRITY_EXCEPTION`.
- Forgetting to set `OwnerId` (Assigned To) → the task may default to the running user instead of the intended owner.
- Leaving Due Date blank when the task is time-sensitive.
