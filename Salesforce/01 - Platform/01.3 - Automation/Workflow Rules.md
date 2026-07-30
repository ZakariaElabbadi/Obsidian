---
tags: [salesforce, platform, concept, automation, legacy]
aliases: [Workflow Rule]
---

# ⏪ Workflow Rules

## 📌 Definition
**Workflow Rule** = an older, simpler automation tool that performs a **single type of action** automatically when a record meets a condition.
(أداة أتمتة قديمة وأبسط، تنفذ نوعًا واحدًا من الإجراءات عند تحقق شرط معين)

> ⚠️ **Legacy tool.** Salesforce now recommends using [[Flow]] for all new automation.
> Workflow Rules still appear in older orgs and sometimes on the Admin exam.
(أداة قديمة، Salesforce توصي الآن باستخدام Flow لكل أتمتة جديدة)

## 🧠 Core Idea
A Workflow Rule answers: **"When this simple condition is met, do ONE simple thing automatically."**
(عندما يتحقق شرط بسيط، نفّذ إجراءً واحدًا بسيطًا تلقائيًا)

```
IF (condition is met)
   → THEN do exactly one action (no branching, no multi-step logic)
```

## 🧾 What a Workflow Rule Can Do (Immediate or Time-Based Actions)
| Action Type | Example |
|---|---|
| Field Update | Set Opportunity.Priority = "High" automatically |
| Email Alert | Send an email when a Case is created |
| Task Creation | Create a follow-up Task for the owner |
| Outbound Message | Send record data to an external system (legacy integration) |

## 💡 Real Example
```
Workflow Rule: "High Value Opportunity Alert"
Condition: Opportunity.Amount > $100,000
Immediate Action: Send Email Alert to Sales Manager
Time-Based Action: 3 days before Close Date → Create Task "Follow up with client"
```
(عندما تتجاوز قيمة الصفقة 100,000 دولار، يُرسل تنبيه فوري ويُنشأ Task قبل موعد الإغلاق بثلاثة أيام)

## ⚖️ Workflow Rule vs Flow — Why Flow Replaced It
| | Workflow Rule | [[Flow]] |
|---|---|---|
| Actions per rule | Only ONE type of action | Multiple actions, any combination |
| Can create records? | ❌ No (except Tasks) | ✅ Yes, any Object |
| Branching logic (IF/ELSE)? | ❌ No | ✅ Yes, full Decision elements |
| Can query related records? | ❌ Very limited | ✅ Yes (Get Records, subqueries) |
| Salesforce's recommendation | ❌ Legacy — being phased out | ✅ Current standard |

(Flow يقدر يفعل كل ما تفعله Workflow Rule وأكثر بكثير، لهذا استبدلها بالكامل)

## ⚠️ Why It Still Matters
- Many **existing orgs** still run old Workflow Rules that haven't been migrated to [[Flow]] yet.
- The Salesforce Admin exam still references it as historical/legacy context.
- Understanding it helps explain **why Flow exists** — Flow was built to overcome these exact limitations.
(فهمه يساعد على فهم لماذا وُجد الـ Flow أصلاً)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Flow]] | The modern replacement — Salesforce recommends migrating all Workflow Rules to Flow |
| [[Objects]] | A Workflow Rule is built for one specific Object |
| [[Fields]] | Conditions and Field Updates are based on Fields |
| [[Validation Rules]] | Different purpose — Validation blocks bad data, Workflow automates a follow-up action |

## ❓ Rule to Remember
> Workflow Rule = **legacy, single-action automation** (أداة قديمة، إجراء واحد فقط)
> IF condition met → ONE action (Field Update, Email Alert, Task, or Outbound Message)
> No branching, no multi-object logic — this is exactly why [[Flow]] replaced it.

---
### 🔗 Related Notes
[[Flow]] | [[Objects]] | [[Fields]] | [[Validation Rules]]
