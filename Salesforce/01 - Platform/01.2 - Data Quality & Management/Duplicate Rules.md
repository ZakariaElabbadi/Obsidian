---
tags: [salesforce, platform, concept, data-management]
aliases: [Duplicate Rule, Matching Rules, Matching Rule]
---

# 👥 Duplicate Rules

## 📌 Definition
**Duplicate Rule** = a rule that checks whether a new or edited record **looks like** an existing one, and decides what to do about it (block or just warn).
(قاعدة تتحقق إن كان السجل الجديد أو المُعدّل يشبه سجلاً موجودًا، وتقرر ماذا تفعل: منع أو تحذير فقط)

> Works together with a **Matching Rule**, which defines **what "similar" means**.
(يعمل مع Matching Rule التي تحدد معنى "التشابه")

## 🧠 Core Idea
Duplicate Rules answer: **"Is someone about to create a record that already exists under a different name/spelling?"**
(هل يوشك أحدهم أن ينشئ سجلاً موجودًا بالفعل بتهجئة مختلفة؟)

## 🧾 Two Parts Working Together
| Part | Role |
|---|---|
| **Matching Rule** | Defines the **logic** for what counts as a duplicate (e.g. same email, similar company name) |
| **Duplicate Rule** | Defines the **action** to take when a match is found (Block / Allow with warning / Report) |

```
Matching Rule  → "Is this a duplicate?"   (the detection logic)
Duplicate Rule → "What do we do about it?" (the response)
```

## 💡 Real Example
```
Matching Rule: "Account Name" is similar (fuzzy match) AND same "Phone"

Duplicate Rule: "Prevent Duplicate Accounts"
Action: Block the save
Message: "A similar Account already exists: Microsoft Corp"
```
A user tries to create `"Microsoft Corp."` while `"Microsoft Corporation"`
already exists with the same phone number — Salesforce **blocks** the save
and shows the existing match.
(يمنع Salesforce الحفظ ويعرض السجل المشابه الموجود بالفعل)

## ⚖️ Duplicate Rule Actions
| Action | Behavior |
|---|---|
| **Block** | Prevents the record from being saved at all |
| **Allow (with alert)** | Lets the user save, but shows a warning first |
| **Report only** | Doesn't interrupt the user — just logs potential duplicates for later review |

## 💡 Where This Matters Most
Duplicate Rules are commonly applied on:
- [[Lead]] — same person submitting the form twice
- [[Account]] — same company entered with slightly different spelling
- [[Contact]] — same person added under two different Accounts by mistake

Remember the earlier lesson rule:
> If Ali leaves and Saad joins the same company, we don't create a new Account — we create a new Contact.

Duplicate Rules help **enforce** that discipline automatically, catching cases
where someone might accidentally create a second Account for the same company.
(تساعد Duplicate Rules على فرض هذا الانضباط تلقائيًا)

## ⚖️ Duplicate Rule vs Validation Rule
| | [[Validation Rules]] | Duplicate Rule |
|---|---|---|
| Checks | Data quality of THIS record (e.g. valid format) | Similarity to OTHER existing records |
| Example | "Phone must be 10 digits" | "This Account looks like one that already exists" |

(Validation Rule يتحقق من جودة بيانات السجل نفسه، بينما Duplicate Rule يتحقق من تشابهه مع سجلات أخرى)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Objects]] | Duplicate Rules are configured per Object (Lead, Contact, Account...) |
| [[Fields]] | Matching Rules compare specific field values |
| [[Import & Export]] | Duplicate Rules also apply during bulk imports, not just manual entry |

## ❓ Rule to Remember
> Matching Rule = defines **what counts as similar** (منطق الكشف)
> Duplicate Rule = defines **what to do about it** — Block, Warn, or Report (رد الفعل)
> Prevents messy data like duplicate Accounts/Contacts/Leads before they happen.

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Validation Rules]] | [[Import & Export]] | [[Lead]] | [[Account]] | [[Contact]]
