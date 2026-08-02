---
tags: [salesforce, admin, flow, get-records]
title: Get Records - Quick Reference
---

# Get Records

## 🎯 What is Get Records?
**Get Records** retrieves one or more records from the Salesforce database.

Use it when you need data that is **not available in `$Record`**.

---

# ✅ When to Use Get Records

Use **Get Records** when:
- You need data from another object.
- You need to retrieve multiple records.
- You need a record that is not available through a relationship.

**Examples:**
- Get the related Account.
- Get all Contacts for an Account.
- Get all Open Opportunities.
- Get a User by Id.

---

# ❌ When NOT to Use Get Records

Do **not** use Get Records if the data is already available.

**Examples:**
```
$Record.Name
$Record.OwnerId
$Record.Account.OwnerId
$Record.Account.Type
```

Always ask yourself:
> Can I access the value directly from `$Record`?

If **Yes**, don't use Get Records.

---

# 🧱 Basic Structure

```
Object
   ↓
Filter Conditions
   ↓
How Many Records to Store
   ↓
How to Store Record Data
```

---

# 🔍 Filter Conditions

**Examples:**
```
Account.Id = $Record.AccountId
User.Id = $Record.OwnerId
Contact.AccountId = $Record.AccountId
```

---

# 📊 How Many Records to Store

## Only the first record
Use when only one record should exist.

**Examples:**
```
Account.Id = $Record.AccountId
User.Id = $Record.OwnerId
```

---

## All Records
Use when multiple records may exist.

**Examples:**
```
Contact.AccountId = $Record.AccountId
Case.ContactId = $Record.Id
```

---

## All Records (Limit)
Retrieve multiple records but limit the result.

**Example:**
```
Get first 10 Open Opportunities
```
Useful for performance.

> You can also set a **Sort Order** (e.g., sort by `CreatedDate DESC`) when retrieving multiple records — helpful for "get the most recent" scenarios.

---

# 💾 How to Store Record Data

## Automatically store all fields
Recommended for beginners.

**Advantages:** Easy, fast to configure
**Disadvantage:** Retrieves every field (less efficient)

---

## Choose fields and let Salesforce do the rest
Retrieve only the fields you need.

Useful for performance.

---

## Choose fields and assign variables (Advanced)
Store each field inside a separate variable.

Usually used in advanced Flows.

---

# 🧭 Decision Rule

Before adding Get Records ask:
```
Can I access the field through $Record?
```
- If **YES** → Don't use Get Records.
- If **NO** → Use Get Records.

---

# 📚 Common Examples

| Traversal | Filter |
|---|---|
| Contact → Account | `Account.Id = $Record.AccountId` |
| Opportunity → Account | `Account.Id = $Record.AccountId` |
| Case → Contact | `Contact.Id = $Record.ContactId` |
| Task → User | `User.Id = $Record.OwnerId` |

---

# ⚠️ Handling "No Record Found"

When using **Only the first record**, Get Records can return **empty/null** if no match exists — the Flow won't error, but any later reference to that record will be blank.

**Always protect against this:**
```
Decision: Is [Get_Records] Null?
   → True  → handle "not found" case (e.g., End, or create a default)
   → False → continue normal path
```

This is especially important before referencing fields from the retrieved record later in the Flow.

---

# 🚦 Governor Limits & Get Records in Loops

> A Flow can run a limited number of SOQL queries per transaction (100 in most contexts).

**❌ Never place Get Records inside a Loop.**
Doing so runs one query per loop iteration — with enough records, this quickly exceeds the SOQL limit and the Flow fails.

**✅ Instead:**
1. Use **one Get Records** to retrieve *all* the records you need as a Collection.
2. **Loop** over that Collection in memory — no additional queries needed.

---

# ✅ Best Practices

- Don't use Get Records if `$Record` already contains the value.
- Retrieve only the data you need.
- Prefer relationship fields when available.
- Use meaningful element names.
- Avoid unnecessary SOQL queries.
- Never call Get Records inside a Loop — retrieve once, loop in memory.
- Add a Null/empty check after "Only the first record" lookups.

---

# ❌ Common Mistakes

- Using Get Records to retrieve the current record.
- Retrieving all records when only one is needed.
- Forgetting to check whether a record was found.
- Using Get Records when a relationship field is available.
- Placing Get Records **inside a Loop** (causes SOQL governor limit errors).

---

# 🧠 Mental Checklist

1. What object started the Flow?
2. Is the data already inside `$Record`?
3. Can I reach it through a relationship?
4. If not, which object should I retrieve?
5. Do I need one record or many?
6. Which fields do I actually need?
7. Could this record possibly not exist? Do I need a Null check?
8. Am I about to put this inside a Loop by mistake?
