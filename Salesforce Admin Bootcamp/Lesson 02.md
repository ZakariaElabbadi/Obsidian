---
tags: [salesforce, admin, ids, lesson02]
title: Lesson 02 - How Salesforce Connects Records
---

# Lesson 02 - How Salesforce Connects Records

## 🎯 Objective
Understand how Salesforce connects records using IDs.

---

# 🧠 Golden Rule
> Salesforce **stores IDs** and **displays Names**.

---

# 📦 Examples

## Account
```
Id   = 001A
Name = Tesla Morocco
```

---

## Contact
```
Name      = Ahmed
AccountId = 001A
```

---

## Opportunity
```
Name      = CRM License
AccountId = 001A
OwnerId   = 005A
```

---

## Task
```
Subject = Call Ahmed
WhoId   = Contact.Id
WhatId  = Opportunity.Id
OwnerId = User.Id
```

---

# ⚠️ Important

Lookup fields store **IDs**, not names.

Examples:
- `AccountId`
- `OwnerId`
- `WhoId`
- `WhatId`
- `CreatedById`
- `LastModifiedById`

---

# 🧠 Mental Model

Salesforce **stores**:
```
001A
```
and **shows**:
```
Tesla Morocco
```

---

# ✅ Key Takeaways

- Every record has a unique **Id**.
- Relationships are built using **IDs**.
- **Names** can change.
- **IDs** never change.
