---
tags: [salesforce, platform, concept]
aliases: [Validation Rule]
---

# ✅ Validation Rules

## 📌 Definition
**Validation Rule** = a check that stops a record from being saved if its data doesn't meet a specific condition.
(قاعدة تمنع حفظ السجل إذا لم تتحقق شروط معينة)

> It's a **quality gate** — it never adds or changes data, it only **blocks** bad data from being saved.
(لا تضيف بيانات، فقط تمنع البيانات الخاطئة من الحفظ)

## 🧠 Core Idea
A Validation Rule answers: **"Is this data acceptable before I let you save it?"**

It's built from two parts:
1. A **formula/condition** that evaluates to TRUE or FALSE
2. An **error message** shown to the user if the condition is TRUE (meaning: something is wrong)

```
IF (condition is TRUE) → block save + show error message
IF (condition is FALSE) → allow save normally
```

## 💡 Example
On the [[Opportunity]] Object:
```
Rule: Close Date cannot be in the past
Formula: CloseDate < TODAY()
Error Message: "Close Date cannot be before today."
```
If a Sales Rep tries to set a Close Date of yesterday, Salesforce blocks the save
and shows the error message.
(إذا حاول موظف المبيعات إدخال تاريخ في الماضي، يمنعه النظام)

## 🧾 Common Real-World Examples
| Object | Rule | Purpose |
|---|---|---|
| [[Opportunity]] | Amount must be greater than 0 | Prevent empty/zero deals |
| [[Account]] | Phone number must contain 10 digits | Ensure valid contact info |
| [[Opportunity Product]] | Discount cannot exceed 30% | Enforce business/pricing policy |
| [[Contact]] | Email field cannot be blank | Ensure every contact is reachable |

## ⚠️ Validation Rule vs Required Field
| | Required Field | Validation Rule |
|---|---|---|
| Purpose | Field must have a value | Field value must meet a **condition** |
| Flexibility | Simple — filled or not | Complex logic (dates, comparisons, combinations) |
| Example | "Email is mandatory" | "Email must end with @company.com" |

(الحقل الإجباري يتحقق فقط من وجود قيمة، بينما Validation Rule تتحقق من صحة القيمة نفسها)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Fields]] | Validation Rules check the values entered into Fields |
| [[Objects]] | A Validation Rule is always attached to one specific Object |
| [[Flow]] | Flows can also enforce logic, but Validation Rules are simpler and run automatically on every save |

## ❓ Rule to Remember
> Validation Rule = a **gatekeeper** (حارس بوابة)
> It doesn't create or change data — it only **blocks** the save if the condition is TRUE.
> Always paired with a clear error message so the user knows what to fix.

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Formula Fields]] | [[Opportunity]] | [[Account]]
