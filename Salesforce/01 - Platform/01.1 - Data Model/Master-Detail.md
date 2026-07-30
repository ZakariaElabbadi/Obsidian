---
tags: [salesforce, platform, concept, relationship]
aliases: [Master-Detail Relationship]
---

# 🔗 Master-Detail

## 📌 Definition
**Master-Detail Relationship** = a **strict, dependent** link between two [[Objects]], where the child (Detail) record **cannot exist** without its parent (Master).
(علاقة صارمة تابعة، السجل التابع لا يمكن أن يوجد بدون السجل الرئيسي)

> Implemented using a special required field on the child object.

## 🧠 Core Idea
Master-Detail answers: **"Does this child record make any sense without its parent?"**
If the answer is **no** — Master-Detail is the right choice.
(إذا كان الجواب لا، فـ Master-Detail هو الخيار الصحيح)

Example:
```
Opportunity (Master)
     │
     ▼  Master-Detail
Opportunity Product (Detail)
```
If the [[Opportunity]] "CRM Project" is deleted, all its [[Opportunity Product]] line items are **deleted too**.
(إذا حُذفت الصفقة، تُحذف كل منتجاتها معها تلقائيًا)
A line item like "Generator 1500kW x2" makes no sense without a deal to belong to.

## 🧾 Key Characteristics
| Property | Behavior |
|---|---|
| Deletion | Deleting the Master deletes all related Detail records (يحذف السجلات التابعة تلقائيًا) |
| Required field? | Always required — cannot be blank |
| Ownership | Detail record has **no owner field** of its own — it inherits from the Master |
| Sharing | Detail automatically inherits the Master's sharing/security settings (يرث إعدادات الأمان) |
| Rollup Summary Fields | ✅ Available — Master can "roll up" totals/counts from its Details |

## 💡 Real Example
```
Opportunity: CRM Project ($50,000)
     │
     ▼ Master-Detail
Opportunity Product: Generator 1500kW  (Qty: 2)
```
The line item **only makes sense** in the context of that specific deal.
Delete the deal → the line item is deleted automatically.
(بدون الصفقة، لا معنى لوجود سطر المنتج)

## 📊 Rollup Summary Fields
Because Detail records are tightly bound to their Master, Salesforce lets the Master
"summarize" its children — e.g., an Opportunity showing:
```
Total Quantity of all Opportunity Products = SUM(Opportunity Product.Quantity)
```
(حقل يجمع أو يعد أو يحسب متوسط بيانات السجلات التابعة تلقائيًا)
This is **not possible** with a plain [[Lookup Relationship]].

## ⚖️ Master-Detail vs Lookup — Quick Comparison
| | Master-Detail | [[Lookup Relationship]] |
|---|---|---|
| Dependency | Child dies with parent (تابع بالكامل) | Independent (مستقل) |
| Required field? | Always required | Optional |
| Deleting parent | Deletes all children | Children survive |
| Rollup Summary | ✅ Available | ❌ Not available |
| Sharing inheritance | ✅ Yes | ❌ No |

*(Full comparison also in [[Difference between master-detail and lookup relationships]].)*

## 🔗 Where This Shows Up in Sales Cloud
- [[Opportunity]] → Master-Detail → [[Opportunity Product]]
- [[Price Book]] → Master-Detail → [[Price Book Entry]] (in most standard setups)

## ❓ Rule to Remember
> Master-Detail = **strict dependency** (علاقة صارمة تابعة)
> Delete the Master → all Details are deleted automatically.
> Use it when the child record has **no meaning on its own**.
> Enables Rollup Summary Fields — something Lookup can never do.

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Lookup Relationship]] | [[Opportunity]] | [[Opportunity Product]] | [[Price Book]] | [[Price Book Entry]]
