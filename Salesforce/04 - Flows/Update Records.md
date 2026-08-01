---
tags: [salesforce, admin, flow, update-records]
title: Update Records - Quick Reference
---

# Update Records

## 🎯 Purpose
Updates an existing record.

---

# ✅ When to Use
Use **Update Records** when a record already exists and you want to change one or more fields.

---

# 🧪 Examples

- Update Opportunity Stage
- Update Account Industry
- Update Contact Phone
- Update Case Status

---

# ❓ Important Question

Before using Update Records, ask:
> "Does the record already exist?"

- **YES** → Update Records
- **NO** → Create Records

---

# 🔧 Two Ways to Update

## 1. Update the Triggering Record Directly
If the Flow is Record-Triggered and you only need to update the **same record** that started the Flow, you don't need to specify which record — Flow already knows it.

```text
Update Records
Object: (automatically the triggering record)
Set: Stage = Closed Won
```

## 2. Update a Different Record (needs a filter)
If you want to update a **related** or **different** record, specify it:

```text
Update Records
Object: Account
Condition: Id = $Record.AccountId
Set: Industry = Food & Beverage
```

---

# 🧩 Common Uses

- Change Stage
- Change Status
- Change Owner
- Change Rating
- Change Close Date

---

# ✅ Best Practices

- Use **Direct Update** whenever the record is already available in the Flow.
- Avoid **Get Records** unless you really need another record.
- If updating records inside a **Loop**, add them to a collection and update the collection **once, after the loop** — don't call Update Records inside the loop (avoids hitting Governor Limits).
- Only set the fields that actually need to change — don't overwrite fields unnecessarily.

---

# ⚠️ Common Mistake

Calling **Update Records** repeatedly inside a Loop instead of updating a collection once after the loop. This can quickly consume Salesforce's DML limits (max 150 DML statements per transaction).

**❌ Wrong:**
```text
Loop
  → Update Records (one at a time)
```

**✅ Correct:**
```text
Loop
  → Add to Collection
End Loop
  → Update Records (collection, once)
```

---

# 📌 Summary

| Element | Meaning |
|---|---|
| **Create Records** | New record |
| **Update Records** | Existing record |
