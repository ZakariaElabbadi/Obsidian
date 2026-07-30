---
tags: [salesforce, platform, concept]
aliases: [Roll-Up Summary Field, Rollup Summary]
---

# ➕ Rollup Summary Field

## 📌 Definition
**Rollup Summary Field** = a special [[Fields|Field]] on the **parent** (Master) record that automatically calculates a value — SUM, COUNT, MIN, or MAX — from its related **child** (Detail) records.
(حقل خاص على السجل الرئيسي (Master) يحسب تلقائيًا قيمة — مجموع، عدد، أصغر، أو أكبر — من سجلاته التابعة)

> Only possible when a [[Master-Detail]] relationship exists between the two Objects.
(لا يمكن إنشاؤه إلا إذا كانت هناك علاقة Master-Detail بين الـ Objectين)

## 🧠 Core Idea
A Rollup Summary Field answers: **"What's the total/count/min/max of all my children's values, without me manually adding them up?"**
(ما هو مجموع/عدد/أصغر/أكبر قيمة لكل السجلات التابعة، دون جمعها يدويًا؟)

## 🧾 The Four Calculation Types
| Type | What It Does | Example |
|---|---|---|
| **SUM** | Adds up a numeric field across all children | Total Amount of all Opportunity Products |
| **COUNT** | Counts how many child records exist | Number of Contacts under an Account |
| **MIN** | Finds the smallest value among children | Earliest Close Date among Opportunities |
| **MAX** | Finds the largest value among children | Highest deal Amount for an Account |

## 💡 Real Example — Exactly What You Already Know
```
Opportunity (Master)
     │
     ▼ Master-Detail
Opportunity Product (Detail)
     Quantity: 2, Total Price: $50,000
     Quantity: 1, Total Price: $10,000
```
On the Opportunity, a Rollup Summary Field can show:
```
Total Line Items Value (SUM) = $60,000
Number of Products (COUNT) = 2
```
The Sales Rep never has to manually add up the line items —
Salesforce keeps this number **automatically up to date**.
(لا يحتاج موظف المبيعات لجمع الأسطر يدويًا، Salesforce يحدّثها تلقائيًا)

## ⚖️ Rollup Summary Field vs Formula Field
| | [[Formula Fields]] | Rollup Summary Field |
|---|---|---|
| Data source | Fields on the **same** record | Fields from **child** records |
| Requires relationship? | No | Yes — must be [[Master-Detail]] |
| Example | `Quantity * Price` on one record | `SUM of Total Price` from all child records |

(Formula Field يحسب من نفس السجل، بينما Rollup Summary يجمع من السجلات التابعة عبر Master-Detail)

## ⚠️ Important Limitation
Rollup Summary Fields **only work with Master-Detail**, not with a plain
[[Lookup Relationship]]. If the relationship is a Lookup, you'd need a
[[Flow]] (or Apex) to simulate the same calculation manually.
(لا تعمل إلا مع Master-Detail، وليس مع Lookup Relationship)

```
✅ Master-Detail → Rollup Summary Field available
❌ Lookup Relationship → must use Flow instead
```

## 💡 Another Common Example
```
Account (Master)
     │
     ▼ Master-Detail-like rollups often simulated for Opportunities (Lookup by default,
       so real orgs typically use a Flow or Report for this instead)
```
⚠️ Note: [[Account]] → [[Opportunity]] is normally a **Lookup**, not Master-Detail —
that's precisely why Sales Managers usually rely on a [[Reports|Report]]
(e.g. "Sum of Opportunity Amount by Account") rather than a native
Rollup Summary Field for that specific relationship.
(هذا بالضبط سبب استخدام Reports بدل Rollup Summary لهذه العلاقة تحديدًا، لأنها Lookup وليست Master-Detail)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Master-Detail]] | Required — Rollup Summary only works on this relationship type |
| [[Formula Fields]] | Similar idea, but calculates within the same record instead of across children |
| [[Junction Object]] | Junction Objects (like Opportunity Product) are common places to roll up totals to their parents |
| [[Reports]] | Common alternative when the relationship is only a Lookup |

## ❓ Rule to Remember
> Rollup Summary Field = **SUM / COUNT / MIN / MAX from child records** (تجميع تلقائي من السجلات التابعة)
> Only works with [[Master-Detail]] relationships — never with plain Lookup.
> Lives on the parent, always shows a live, auto-updating result.

---
### 🔗 Related Notes
[[Master-Detail]] | [[Formula Fields]] | [[Junction Object]] | [[Opportunity]] | [[Opportunity Product]] | [[Reports]]
