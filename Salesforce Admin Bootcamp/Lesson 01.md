---
tags: [salesforce, admin, core-objects, lesson01]
title: Lesson 01 - Salesforce Core Objects
---

# Lesson 01 - Salesforce Core Objects

## 🎯 Objective
Understand the five most important Salesforce standard objects.

---

# 📦 Core Objects

## User
A person who can log in to Salesforce.

**Examples:**
- Zakaria
- Sara

---

## Account
Represents a company.

**Example:**
- Tesla Morocco

---

## Contact
Represents a person who works for an Account.

**Example:**
- Ahmed Benali

---

## Opportunity
Represents a potential sales deal.

**Example:**
- CRM License ($10,000)

---

## Task
Represents an activity.

**Example:**
- Call Ahmed

---

# 🔗 Relationships

```
User
└── Owns → Opportunity

User
└── Owns → Task

Account
├── Has Many → Contacts
└── Has Many → Opportunities

Contact
└── Belongs To → Account

Opportunity
└── Belongs To → Account

Task
├── Who   → Contact
├── What  → Opportunity
└── Owner → User
```

---

# ✅ Key Takeaways

| Object | Represents |
|---|---|
| **User** | Employee |
| **Account** | Company |
| **Contact** | Person |
| **Opportunity** | Sales Deal |
| **Task** | Activity |
