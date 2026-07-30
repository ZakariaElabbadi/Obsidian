---
tags: [salesforce, sales-cloud, object]
aliases: [Person, Individual]
---

# 👤 Contact

## 📌 Definition
**Contact** = the **Person** inside a Company.
الشخص داخل الشركة

> Contact answers one question only:
> **"Who do we talk to?"**

## 🧠 Core Idea
A Contact is always linked to an [[Account]].
A person without a company context is usually a [[Lead]] — once confirmed, they become a Contact tied to an Account.
الشخص لا يوجد بمفرده، بل مرتبط دائمًا بشركة

## 🔄 Where Does It Come From?
A Contact is usually created when a [[Lead]] is **Converted**.

```
Lead
 │
 │ Convert
 ▼
Contact   ← the Person (الشخص)
    │
    └── linked to → Account (الشركة)
```

## 🔗 Relationship to Other Objects
| Relationship | Description |
|---|---|
| Account → Contact | One Account can have **many** Contacts (people who work there) |
| Contact → Opportunity | A Contact can be linked to an Opportunity as the person we negotiate with |

```
Account (Microsoft)
   │
   ├── Contact: Ahmed   ← the person we negotiate with
   │
   └── Opportunity: CRM Project
```

## ⚠️ Important Rule
**People change more often than companies.**
الأشخاص يتغيرون أكثر من الشركات

Example:
> Ali (Contact) leaves Microsoft, Saad joins.
> - ❌ We do NOT create a new Account
> - ✅ We DO create a new Contact for Saad
> - ✅ Ali's old Contact record stays as history (or gets marked inactive)

## 💡 Real Example
> Ahmed works at Microsoft.
> He is the person emailing us, negotiating price, and signing the deal.
>
> - Microsoft = [[Account]] (the company)
> - Ahmed = **Contact** (the person)
> - CRM Project = [[Opportunity]] (the deal)

```
Microsoft (Account)
   │
   ├── Ahmed (Contact)
   │
   └── CRM Project (Opportunity)
```

## ❓ Rule to Remember
> Account = the Company (لا يتغير غالبًا)
> Contact = the Person inside it (يتغير كثيرًا)
> Same company, different person → same Account, new Contact.

---
### 🔗 Related Notes
[[Lead]] | [[Account]] | [[Opportunity]]
