---
tags: [salesforce, platform, concept, data-management]
aliases: [External ID Field]
---

# 🆔 External ID

## 📌 Definition
**External ID** = a special [[Fields|Field]] marked to hold a **unique identifier from an outside system**, used to match records between Salesforce and that system.
(حقل خاص يُعلَّم لتخزين معرّف فريد من نظام خارجي، يُستخدم لمطابقة السجلات بين Salesforce وذلك النظام)

> Salesforce has its own internal Record ID for every record — External ID
> is a **second identifier**, borrowed from another system (like SAP, an
> old CRM, or an e-commerce platform).
(Salesforce لديه معرّف داخلي خاص به لكل سجل، والـ External ID معرّف إضافي مستعار من نظام آخر)

## 🧠 Core Idea
External ID answers: **"How do I match a record coming from an outside system to the correct existing Salesforce record — without relying on Salesforce's own internal ID?"**
(كيف أطابق سجلًا قادمًا من نظام خارجي مع السجل الصحيح في Salesforce، دون الاعتماد على المعرّف الداخلي لـ Salesforce؟)

## 💡 Real Example
```
Old CRM system has: Customer_ID = "CUST-4521" for Microsoft

In Salesforce, Account has a custom field:
Legacy_Customer_ID__c   (marked as External ID)
Value: "CUST-4521"
```
Now, every time data syncs from the old CRM, Salesforce can find the
**exact matching Account** using `CUST-4521`, instead of guessing based
on the company name (which might be spelled differently).
(بدل التخمين بناءً على اسم الشركة الذي قد يُكتب بشكل مختلف، يُستخدم المعرّف الدقيق للمطابقة)

## ⚙️ Where It's Used Most — Upsert
Remember **Upsert** from [[Import & Export]]:
> Update if the record already exists, Insert if it doesn't.

External ID is **what makes Upsert possible**. Without a unique External ID
field, Salesforce has no reliable way to know "this incoming row already
exists — update it" versus "this is brand new — create it."
(بدون External ID، لا توجد طريقة موثوقة لمعرفة أن هذا السجل موجود بالفعل أم جديد)

```
Import file has 10,000 rows from an external ERP system
     │
     ▼ Match by External ID field
Existing Salesforce records → UPDATED
New records (no match found) → INSERTED
```

## 🧾 Key Properties of an External ID Field
| Property | Behavior |
|---|---|
| Must be unique? | Can be marked "Unique" to prevent duplicates |
| Field types allowed | Text, Number, Email |
| Used for | Upsert operations, data migrations, ongoing integrations |
| Indexed automatically | Salesforce indexes it for faster lookups during import |

## ⚖️ External ID vs Salesforce Record ID
| | Salesforce Record ID | External ID |
|---|---|---|
| Created by | Salesforce automatically | Admin, mapped from an outside system |
| Format | Salesforce's own 15/18-character ID | Whatever format the external system uses |
| Purpose | Internal reference within Salesforce | Matching/syncing with external systems |

(المعرّف الداخلي يُنشئه Salesforce تلقائيًا، بينما External ID يُعرّفه الـ Admin ليطابق نظامًا خارجيًا)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Fields]] | External ID is a property/setting applied to a regular Field |
| [[Import & Export]] | Essential for Upsert operations during bulk imports |
| [[Objects]] | Any Object can have one or more External ID fields |
| [[Duplicate Rules]] | External ID is a more precise alternative to fuzzy-matching for detecting duplicates from external sources |

## ❓ Rule to Remember
> External ID = **a field storing another system's unique identifier** (حقل يخزن معرّفًا من نظام خارجي)
> Makes **Upsert** possible — the key to smart, safe bulk imports.
> Different from Salesforce's own Record ID, which is internal and automatic.

---
### 🔗 Related Notes
[[Fields]] | [[Import & Export]] | [[Objects]] | [[Duplicate Rules]]
