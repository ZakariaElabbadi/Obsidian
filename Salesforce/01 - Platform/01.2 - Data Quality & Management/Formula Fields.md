---
tags: [salesforce, platform, concept]
aliases: [Formula Field]
---

# 🧮 Formula Fields

## 📌 Definition
**Formula Field** = a special type of [[Fields|Field]] whose value is **automatically calculated**, never typed in manually.
(حقل تُحسب قيمته تلقائيًا، ولا يُدخلها المستخدم يدويًا)

> Read-only by nature — a user can never edit a Formula Field directly.
(للقراءة فقط، لا يمكن للمستخدم تعديله مباشرة)

## 🧠 Core Idea
A Formula Field answers: **"Can this value be derived from other data I already have?"**
If yes — don't store it manually, **calculate it**.
(إذا كانت القيمة يمكن استنتاجها من بيانات أخرى، لا تُخزّنها يدويًا، بل احسبها)

## 💡 Example
On [[Opportunity Product]]:
```
Quantity = 2
Unit Price = $25,000

Formula Field: Total Price = Quantity * Unit Price
Result: $50,000   (calculated automatically, always up to date)
```
If the Quantity changes to 3, the Total Price **updates instantly** — no one needs to recalculate it.
(إذا تغيرت الكمية، يتحدث السعر الإجمالي فورًا دون تدخل بشري)

## 🧾 Common Real-World Examples
| Object | Formula Field | Formula Logic |
|---|---|---|
| [[Opportunity]] | Days Until Close | `CloseDate - TODAY()` |
| [[Contact]] | Full Name | `FirstName & " " & LastName` |
| [[Opportunity Product]] | Total Price | `Quantity * UnitPrice` |
| [[Account]] | Is VIP Customer | `IF(AnnualRevenue > 1000000, TRUE, FALSE)` |

## ⚠️ Formula Field vs Rollup Summary Field
| | Formula Field | Rollup Summary Field |
|---|---|---|
| Data source | Fields on the **same** record | Fields from **child** records (via [[Master-Detail]]) |
| Example | `Quantity * Price` on one record | `SUM of all Opportunity Product prices` on the parent Opportunity |
| Relationship needed? | No | Yes — requires Master-Detail |

(Formula Field يحسب من نفس السجل، بينما Rollup Summary يجمع من السجلات التابعة)

## ⚙️ Where This Shows Up
```
Opportunity Product
     │
     ▼ Formula Field
Total Price = Quantity × Unit Price
```
This is exactly why, in the Flow we discussed earlier, once
`Get Price Book Entry` returns the price, the Total on the
[[Opportunity Product]] can be calculated automatically instead
of being entered manually.
(بدل إدخال السعر الإجمالي يدويًا، يُحسب تلقائيًا عبر Formula Field)

## ❓ Rule to Remember
> Formula Field = **calculated, not typed** (محسوب وليس مُدخلًا)
> Always read-only.
> Updates automatically whenever the fields it depends on change.
> Different from Rollup Summary — Formula works within the **same record**, Rollup pulls from **child records**.

---
### 🔗 Related Notes
[[Fields]] | [[Objects]] | [[Master-Detail]] | [[Validation Rules]] | [[Opportunity Product]]
