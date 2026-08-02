---
tags: [salesforce, admin, flow, create-records]
title: Create Records - Quick Reference
---

# Create Records

## 🎯 Purpose
Creates one or more new records.

---

# 📦 Can Create

- Task
- Contact
- Opportunity
- Case
- Account
- Custom Objects

---

# ✅ Required

1. Select Object
2. Fill required fields

---

# 🔢 Single Record vs. Multiple Records

The **Create Records** element has two modes:

| Mode | Use When |
|---|---|
| **One record** | You're creating a single record (e.g., one Task) |
| **Multiple records** | You're creating many records at once from a **Collection Variable** (e.g., a Task for every Contact in a list) |

> Creating from a **Collection** is far more efficient than looping and calling Create Records inside the loop — it sends all records in **one single operation** (bulkified), avoiding governor limit issues.

---

# 🧪 Example

```text
Object: Task
Subject: Call New Lead
Assigned To: Lead Owner
WhoId: Lead Id
```

---

# 🆔 Getting the ID of the Created Record

After Create Records runs, Flow can store the **Id** of the new record in a variable, so you can use it later in the same Flow (e.g., to create a related child record, or to update it).

**Example:**
```text
Create Records → Contact
Store result in: varNewContactId
     ↓
Use varNewContactId as WhoId in the next Create Records (Task)
```

---

# 📝 Notes

> **Create Records** always **INSERTS** a new record.
> It **never** updates existing records — use **Update Records** for that.

---

# ✅ Best Practices

- Whenever possible, **build a collection first** and create all records in **one Create Records element** — not one per loop iteration.
- Only fill in the fields you actually need; don't hardcode values that should come from `$Record` or a variable.
- If you need the new record's Id afterward, make sure to store the Create Records output in a variable.

# ❌ Common Mistakes

- Placing **Create Records inside a Loop** when a **Collection + single Create Records after the loop** would work — this wastes DML operations and can hit governor limits on large data volumes.
- Forgetting a **required field** on the target object → the Flow fails at runtime with a validation/required-field error.
- Confusing **Create Records** with **Update Records** when the intent was actually to modify an existing record.
