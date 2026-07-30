---
tags: [salesforce, platform, concept, relationship]
aliases: [Lookup Field, Lookup]
---

# 🔍 Lookup Relationship

## 📌 Definition
**Lookup Relationship** = a loose link between two [[Objects]], where one record **points to** another, but they can exist **independently**.
(علاقة مرنة بين Objectين، السجل يشير إلى الآخر لكن يمكن أن يوجدا بشكل مستقل)

> Implemented using a special **Lookup Field** (a type of [[Fields|Field]]).

## 🧠 Core Idea
A Lookup Relationship answers: **"Which record does this one relate to?"** — without forcing dependency.
(يربط بين سجلين، لكن دون إجبارية الوجود المشترك)

Example:
```
Contact (Ahmed)
     │
     ▼  Lookup: Account
Account (Microsoft)
```
If `Microsoft` (the Account) gets deleted, `Ahmed` (the Contact) can still exist —
the Lookup field on Ahmed simply becomes empty.
(إذا حُذفت الشركة، يبقى الشخص موجودًا، فقط يصبح الحقل فارغًا)

## 🧾 Key Characteristics
| Property | Behavior |
|---|---|
| Deletion | Deleting the parent does **not** delete the child (لا يحذف السجل التابع) |
| Required? | Optional by default — can be made required |
| Ownership | Child record has its **own** owner, independent of the parent |
| Sharing | Child does **not** automatically inherit the parent's sharing/security settings |
| Rollup Summary Fields | ❌ Not supported (unlike Master-Detail) |

## 💡 Real Example
```
Case (Object)
     │
     ▼ Lookup: Contact
Contact (Ahmed)
```
A Case is linked to a Contact, but if Ahmed's Contact record is later deleted,
the Case can remain in the system (with the lookup field cleared).
(الـ Case يمكن أن يبقى حتى لو حُذف الشخص المرتبط به)

## ⚖️ Lookup vs Master-Detail — Quick Comparison
| | Lookup Relationship | [[Master-Detail]] |
|---|---|---|
| Dependency | Independent (مستقل) | Dependent — child dies with parent (تابع) |
| Required field? | Optional | Always required |
| Deleting parent | Child survives | Child is deleted too |
| Rollup Summary | ❌ Not available | ✅ Available |
| Sharing inheritance | ❌ No | ✅ Yes, child inherits parent's security |

*(See [[Master-Detail]] and [[Difference between master-detail and lookup relationships]] for the full comparison.)*

## 🔗 Where This Shows Up in Sales Cloud
Almost every relationship you've studied so far is a **Lookup Relationship**:
- [[Contact]] → looks up to → [[Account]]
- [[Opportunity]] → looks up to → [[Account]]
- [[Case]] → looks up to → [[Contact]] / [[Account]]

## ❓ Rule to Remember
> Lookup = **flexible connection** (علاقة مرنة)
> Parent can be deleted without deleting the child.
> Used when two records are related, but **not dependent** on each other's existence.

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Master-Detail]] | [[Account]] | [[Contact]] | [[Opportunity]]
