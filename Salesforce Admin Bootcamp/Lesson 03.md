---
tags: [salesforce, admin, flow, lesson03]
title: Salesforce Flow - Lesson 3
date: 2026-07-31
---

# Salesforce Flow - Lesson 3
**Date:** 2026-07-31

---

# 🧩 Main Concepts

## 1. Child → Parent (Direct Access)

If the current record contains a Lookup or Master-Detail field, you can access the parent **directly**.

**Examples:**

Opportunity → Account
```text
$Record.Account.Name
```

Opportunity → Owner
```text
$Record.Owner.Email
```

Opportunity → Owner → Manager
```text
$Record.Owner.Manager.Name
```

> No **Get Records** is needed.

---

## 2. Parent → Children (Get Records)

A parent can have many children.

**Examples:**
- Account → Contacts
- Account → Opportunities
- User → Tasks

Because there are multiple child records, Flow doesn't know which one you want.

Use:
- **Get Records**
- **Filter**
- **Loop** (if processing multiple records)

---

## 3. Record IDs

Relationships are built using **IDs**.

```text
Opportunity.AccountId = Account.Id
```
The value stored in `AccountId` is the ID of the related Account.

```text
Task.OwnerId = User.Id
```

---

## 4. Create Records

Use **Create Records** when you want to create a new record.

**Examples:**
- Create Task
- Create Contact
- Create Case

---

## 5. Update Records

Use **Update Records** when you want to modify an existing record.

**Examples:**
- Update Account Industry
- Update Opportunity Stage
- Update Contact Phone

---

## 6. Updating a Related Record

**Current Object:** Opportunity
**Update:** Account

```text
Object: Account
Condition: Id = $Record.AccountId
```

Then update any Account fields.

**Example:**
```text
Industry = Food & Beverage
Account Type = Customer - Direct
```

---

## 7. Decision = IF

**Programming:**
```text
if (Amount > 10000)
```

**Flow:** Decision Element

**Example:**
```text
Outcome: High Amount
Condition: $Record.Amount > 10000
```

- If **TRUE** → Create Task → Update Account
- If **FALSE** → End

---

## 8. Flow We Built

```text
Start (Opportunity Created)
        │
        ▼
Create Task
        │
        ▼
Update Account
        │
        ▼
End
```

---

# 📏 Rules to Remember

- ✅ Child → Parent = Direct
- ❌ Child → Parent = No Get Records
- ✅ Parent → Children = Get Records
- ✅ Create Records = New Record
- ✅ Update Records = Existing Record
- ✅ Relationships are connected using IDs.

---

# 📝 Homework

Create a **Record-Triggered Flow**:

**Trigger:** Opportunity Created

```text
IF Amount > 10000
THEN
  - Create Task
  - Update Account Industry
  - Update Account Type
OTHERWISE
  - Do nothing
```
