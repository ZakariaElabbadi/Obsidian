---
tags: [salesforce, platform, concept, security]
aliases: [Data Security, Sharing Model, Salesforce Security]
---

# 🔐 Security Model

## 📌 Definition
**Security Model** = the layered system that controls **who can see and do what** with data in Salesforce.
(النظام متعدد الطبقات الذي يحدد من يرى البيانات وماذا يستطيع أن يفعل بها)

> It's not one setting — it's **several layers stacked together**, each answering a different question.
(ليس إعدادًا واحدًا، بل عدة طبقات مجتمعة معًا)

## 🧠 Core Idea
Security in Salesforce works at **two levels**:
1. **Object & Field level** — what CAN a user do, in general? (covered by [[Profiles]] & [[Permission Sets]])
2. **Record level** — of the records they're allowed to touch, WHICH ONES can they actually see?
(المستوى الأول: ماذا يستطيع أن يفعل بشكل عام؟ المستوى الثاني: أي سجلات تحديدًا يمكنه رؤيتها؟)

This note focuses on the **record-level** layers — the part most people call "the Security Model."

## 🧾 The Layers, in Order
```
1. Organization-Wide Defaults (OWD)
        │  sets the baseline (most restrictive starting point)
        ▼
2. Role Hierarchy
        │  opens access upward (managers see their team's records)
        ▼
3. Sharing Rules
        │  opens access for specific groups/criteria (exceptions)
        ▼
4. Manual Sharing
        │  opens access for one specific record, one specific user
        ▼
= Final record-level access a user has
```
Each layer can only **add** more access — never take away what came before.
(كل طبقة تضيف صلاحية فقط، لا تسحب صلاحية سابقة)

## 1️⃣ Organization-Wide Defaults (OWD)
The **baseline / starting point** — the most restrictive setting for each [[Objects|Object]].
(الإعداد الافتراضي والأكثر تقييدًا لكل Object)

| Setting | Meaning |
|---|---|
| **Private** | Only the record owner (and their managers, via Role Hierarchy) can see it |
| **Public Read Only** | Everyone can view, only the owner can edit |
| **Public Read/Write** | Everyone can view and edit |

💡 Example:
```
Opportunity OWD = Private
→ By default, a Sales Rep can only see THEIR OWN Opportunities.
```

## 2️⃣ Role Hierarchy
Automatically gives **managers** visibility into records owned by people **below them**.
(يمنح المدراء رؤية تلقائية على سجلات موظفيهم)

```
Sales Manager (Role)
      │
      ▼
Sales Rep (Role)
```
If OWD = Private, a Sales Rep only sees their own Opportunities —
but their **Sales Manager** automatically sees theirs too, because
of the Role Hierarchy.
(المدير يرى تلقائيًا سجلات من هم أسفله في التسلسل الهرمي)

## 3️⃣ Sharing Rules
**Exceptions** that open up access beyond OWD and Role Hierarchy —
based on **who owns the record** or **criteria on the record**.
(استثناءات تفتح صلاحيات إضافية بناءً على المالك أو شروط في السجل)

💡 Example:
```
Sharing Rule: "Share all Opportunities where Region = 'Morocco'
               with the 'Morocco Support Team' group"
```
This lets a whole team see records they wouldn't normally have access to,
without changing OWD for everyone.
(يسمح لفريق كامل برؤية سجلات معينة دون تغيير الإعداد العام للجميع)

## 4️⃣ Manual Sharing
A user manually shares **one specific record** with **one specific person**
(via the "Sharing" button on a record).
(مشاركة سجل واحد فقط مع شخص واحد، يدويًا)

💡 Example:
```
Ahmed shares HIS Opportunity "CRM Project" with Sara,
who normally wouldn't be able to see it.
```

## ⚖️ Object/Field Permissions vs Record-Level Sharing
| | [[Profiles]] / [[Permission Sets]] | Security Model (this note) |
|---|---|---|
| Controls | Can the user use this Object/Field at all? | Which specific **records** can they see? |
| Example | "Can Sales Reps see the Opportunity object?" | "Which Opportunity records can THIS Sales Rep see?" |
| Level | Object & Field | Record |

(Profile يحدد هل يستطيع استخدام الـ Object، بينما Security Model يحدد أي سجلات بالضبط يراها)

## 💡 Full Example Combining Everything
```
Object: Opportunity
OWD: Private                          → nobody sees anyone else's deals by default
Role Hierarchy: Sales Manager > Rep    → managers see their reps' deals
Sharing Rule: Region = Morocco team    → whole regional team sees Morocco deals
Manual Share: Ahmed → Sara (one deal)  → Sara sees just that one extra deal
```

## ❓ Rule to Remember
> Security Model = **layered, record-level visibility**
> Start restrictive with **OWD**, then open up with **Role Hierarchy**, **Sharing Rules**, and **Manual Sharing**.
> Different from [[Profiles]]/[[Permission Sets]], which control access to the Object/Field itself, not which records.

---
### 🔗 Related Notes
[[Profiles]] | [[Permission Sets]] | [[Objects]] | [[Fields]]
