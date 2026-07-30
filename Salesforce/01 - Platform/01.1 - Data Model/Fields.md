---
tags: [salesforce, platform, concept]
aliases: [Field Types, Columns]
---

# 🧱 Fields

## 📌 Definition
**Field** = a single piece of data stored inside an [[Objects|Object]].
(عمود يخزن قطعة واحدة من البيانات)

> If an Object is a table, a Field is one **column** in that table.

## 🧠 Core Idea
Every property you want to track about a record needs its own **Field**.
(كل معلومة تريد تتبعها تحتاج حقلًا خاصًا بها)

Example — the [[Account]] Object has fields like:
| Field | Value |
|---|---|
| Account Name | Microsoft |
| Industry | Technology |
| Phone | +1 800 000 0000 |
| Billing Address | Redmond, USA |

Each of these is a separate **Field**, but together they describe **one Account record**.

## 🧾 Common Field Types
| Type | Example | Notes |
|---|---|---|
| Text | Account Name | Free text (نص حر) |
| Number | Amount | Numeric values |
| Currency | Opportunity Amount | Number formatted as money |
| Date / Date-Time | Close Date | Calendar values |
| Picklist | Stage (Prospecting, Closed Won...) | Fixed list of options (قائمة خيارات ثابتة) |
| Checkbox | Active | True / False |
| Lookup | Account on Contact | Points to another record — see [[Lookup Relationship]] |
| Formula | Total Price | Auto-calculated — see [[Formula Fields]] |

## ⚠️ Standard vs Custom Fields
| Type | Description |
|---|---|
| **Standard Field** | Comes built-in (e.g. `Name`, `CreatedDate`) |
| **Custom Field** | Created by an Admin, always ends with `__c` (e.g. `Warranty_End_Date__c`) |

(نفس منطق Standard Object و Custom Object، لكن على مستوى الحقل)

## 💡 Example
On the [[Opportunity]] Object:
```
Standard Fields: Name, Amount, Stage, Close Date
Custom Field:    Discount_Percentage__c   ← created by the Admin
```

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Objects]] | A Field always belongs to exactly one Object |
| [[Validation Rules]] | Check the value entered into a Field before saving |
| [[Formula Fields]] | A special Field type that auto-calculates its value |
| [[Lookup Relationship]] / [[Master-Detail]] | Special Field types that connect two Objects |

## ❓ Rule to Remember
> Object = the table
> **Field = the column** (one piece of data)
> Record = the row (a full set of field values)
>
> Field Type decides what kind of data can go in — text, number, date, picklist, or a link to another record.

---
### 🔗 Related Notes
[[Objects]] | [[Lookup Relationship]] | [[Master-Detail]] | [[Validation Rules]] | [[Formula Fields]]
