---
tags: [salesforce, platform, concept, automation]
aliases: [Approval Processes]
---

# ✋ Approval Process

## 📌 Definition
**Approval Process** = an automated series of steps to get a record **approved or rejected** by one or more people, before something is allowed to proceed.
(سلسلة خطوات آلية للحصول على موافقة أو رفض سجل من شخص أو أكثر قبل المتابعة)

> Think of it as a **formal sign-off workflow** built into Salesforce.
(سير عمل رسمي للموافقات مدمج داخل Salesforce)

## 🧠 Core Idea
An Approval Process answers: **"This action needs a human decision-maker to say yes before it happens — how do we route it to the right person automatically?"**
(هذا الإجراء يحتاج قرارًا بشريًا قبل أن يحدث، كيف نوجهه تلقائيًا للشخص المناسب؟)

## 🧾 Key Components
| Component | Purpose |
|---|---|
| **Entry Criteria** | Which records trigger the approval? (e.g. Discount > 20%) |
| **Approval Steps** | Who needs to approve? Can be one person or a chain of people |
| **Approver** | A specific user, the record owner's manager, or a queue |
| **Actions on Approval** | What happens if approved? (e.g. update Stage, send email) |
| **Actions on Rejection** | What happens if rejected? (e.g. notify Sales Rep, revert a field) |
| **Final Actions** | Lock the record, update a field, send notifications |

## 💡 Real Example
```
Approval Process: "Opportunity Discount Approval"

Entry Criteria: Opportunity.Discount__c > 20%

Step 1: Approver = Record Owner's direct Manager
   ↓ Approved
Step 2: Approver = Regional Sales Director (if discount > 40%)
   ↓ Approved
Final Action: Update Opportunity.Status = "Approved"
              Unlock record for editing
```
A Sales Rep tries to apply a 35% discount on an [[Opportunity]] — the record
is automatically **locked** and routed to their manager for approval before
the deal can move to "Closed Won."
(السجل يُقفل تلقائيًا ويُرسل للمدير للموافقة قبل أن تكتمل الصفقة)

## ⚖️ Approval Process vs Flow
| | [[Flow]] | Approval Process |
|---|---|---|
| Purpose | General automation (any logic) | Specifically routes records for human approval |
| Human decision needed? | Not necessarily | Always — someone must click Approve/Reject |
| Locks records? | Only if built to | Can automatically lock the record during review |
| Multi-step chains of people | Possible, but manual to build | Built-in support for approval chains |

(Flow لأتمتة عامة، بينما Approval Process مخصص لتوجيه الموافقات البشرية)

## 🔒 Record Locking
While a record is pending approval, it's usually **locked** — meaning
no one (not even the owner) can edit it until the approval finishes.
(أثناء انتظار الموافقة، يُقفل السجل ولا يمكن لأحد تعديله)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Objects]] | An Approval Process is built for one specific Object |
| [[Fields]] | Entry criteria and actions are based on field values |
| [[Validation Rules]] | Both can block changes, but Validation Rules check data quality, Approval Process checks human sign-off |
| [[Flow]] | Can trigger a Flow as part of the approval's final actions |

## ❓ Rule to Remember
> Approval Process = **formal human sign-off workflow** (موافقة رسمية بشرية)
> Entry Criteria decides which records need approval, Steps decide who approves.
> Records are typically locked while pending — no edits allowed until resolved.
> Different from [[Flow]]: Flow automates logic, Approval Process specifically routes decisions to people.

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Flow]] | [[Validation Rules]] | [[Opportunity]]
