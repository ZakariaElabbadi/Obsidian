---
tags: [salesforce, platform, concept, relationship, flow]
aliases: [Relationship Traversal, Parent-Child Navigation, Related Records]
---

# 🧭 Object Relationship Traversal

## 📌 Definition
**Relationship Traversal** = the technique of moving from one record to a **related** record — either upward to its parent, or downward to its children — using the relationship that connects them.
(تقنية الانتقال من سجل إلى سجل مرتبط به، إما صعودًا إلى السجل الرئيسي أو نزولًا إلى السجلات التابعة، عبر العلاقة التي تربطهما)

> This is the **single most important skill** for building Flows that
> touch more than one Object — which is almost every real Flow.
(هذه أهم مهارة على الإطلاق لبناء Flows تتعامل مع أكثر من Object، وهو ما يحدث في كل Flow حقيقي تقريبًا)

## 🧠 The Two Directions — This Is the Whole Concept
Every relationship (built with [[Lookup Relationship]] or [[Master-Detail]])
can be traveled in **two directions**:

```
              ▲
              │   Child → Parent
              │   ("go UP to the one record I point to")
              │
         [Contact] ────Lookup: AccountId────► [Account]
              │
              │   Parent → Child
              │   ("go DOWN to the many records that point to me")
              ▼
```

| Direction | Question It Answers | How Many Records? |
|---|---|---|
| **Child → Parent** | "Which Account does this Contact belong to?" | Exactly ONE (a single lookup) |
| **Parent → Child** | "Which Contacts belong to this Account?" | MANY (a list/collection) |

This single distinction — **one record vs. many records** — is why the two
directions are built completely differently in both SOQL and Flow.
(هذا الفرق: سجل واحد مقابل عدة سجلات، هو سبب اختلاف طريقة البناء في الاتجاهين)

## 🧾 Direction 1: Child → Parent (Going Up)
Every child record has a **Lookup field** that stores the ID of its one parent.
(كل سجل تابع لديه حقل Lookup يخزن معرّف السجل الرئيسي الوحيد)

### In SOQL — dot notation
```sql
SELECT Name, Account.Name, Account.Industry
FROM Contact
```
You just "dot into" the parent field. Easy, because there's only **one** parent.
(تكتب نقطة ثم اسم الحقل، سهل لأن هناك أب واحد فقط)

### In Flow
When you use **Get Records** to fetch a Contact, the related Account is
accessed through the lookup relationship field directly:
```
{!Get_Contact.Account.Name}
```
Because it's a single record, Flow lets you reference it directly —
no loop needed.
(لأنه سجل واحد فقط، لا تحتاج Loop للوصول إليه)

## 🧾 Direction 2: Parent → Child (Going Down)
A parent doesn't "know" its children directly — Salesforce finds them by
searching: *"which child records have MY ID in their lookup field?"*
(الأب لا "يعرف" أبناءه مباشرة، Salesforce يبحث عن كل سجل تابع يحمل معرّف الأب في حقل الـ Lookup الخاص به)

### In SOQL — subquery (Related List name, plural)
```sql
SELECT Name, (SELECT Name, Email FROM Contacts)
FROM Account
```
Notice `Contacts` is **plural** — because there can be many.
This plural name is called the **Child Relationship Name**.
(اسم الجمع هنا يسمى Child Relationship Name)

### In Flow — you need a SEPARATE "Get Records"
Unlike the Child→Parent direction, Flow **cannot** just "dot down" to
children automatically. You must add a new **Get Records** element,
filtered by the parent's ID:
```
Get Records: Object = Contact
Filter: AccountId Equals {!Get_Account.Id}
→ Store in a Collection Variable (because there can be many)
```
Then, to work with each one, you typically add a **Loop** element.
(يجب استخدام Get Records منفصل مفلتر بمعرّف الأب، ثم Loop للتعامل مع كل سجل)

## 🔑 The #1 Rule for Flows
> **Going UP (Child → Parent) = direct reference, no loop needed.**
> **Going DOWN (Parent → Child) = separate Get Records + Loop, because there can be many.**
(الصعود = مرجع مباشر بدون Loop. النزول = Get Records منفصل + Loop لأن العدد قد يكون كبيرًا)

## 💡 Full Walkthrough — The Exact Flow You Studied
Let's trace the classic Flow using this concept:
```
Opportunity (parent)
     │
     ▼ Parent → Child (needs separate Get Records)
Get Records: Opportunity Product
Filter: OpportunityId = {!Get_Opportunity.Id}
     │
     ▼ for each Opportunity Product, go Child → Parent (direct reference)
{!Loop.PriceBookEntryId.Product2.Name}
{!Loop.PriceBookEntryId.UnitPrice}
```
- Fetching all **Opportunity Products** of one Opportunity = Parent→Child (Get Records + Loop)
- Reading the **Product name** or **Price** from each line's Price Book Entry = Child→Parent (direct dot access)

This is exactly why the original Flow needed **Get Price Book → Get Product
→ Get Price Book Entry** as *separate* steps — each one either fetches a
list (Parent→Child) or reads a related field (Child→Parent), and they
can't be skipped or merged.
(هذا بالضبط سبب حاجة الـ Flow الأصلي لخطوات منفصلة: كل خطوة إما تجلب قائمة أو تقرأ حقلاً مرتبطًا)

## 🧾 Quick Reference Table
| Scenario | Direction | SOQL | Flow |
|---|---|---|---|
| Get a Contact's Account name | Child → Parent | `Account.Name` | `{!Get_Contact.Account.Name}` |
| Get all Contacts of an Account | Parent → Child | `(SELECT Name FROM Contacts)` | New Get Records, filter by AccountId, + Loop |
| Get an Opportunity Product's Product name | Child → Parent | `PricebookEntry.Product2.Name` | `{!Loop.PriceBookEntryId.Product2.Name}` |
| Get all Opportunity Products of an Opportunity | Parent → Child | `(SELECT Name FROM OpportunityLineItems)` | New Get Records, filter by OpportunityId, + Loop |

## ⚠️ Common Beginner Mistake
Trying to access children directly like a parent field:
```
❌ {!Get_Account.Contacts}   ← this does NOT work in Flow
```
Flow has no automatic "list of children" reference. You must **always**
add a dedicated Get Records element filtered by the parent's ID when
going Parent→Child.
(Flow لا يملك مرجعًا تلقائيًا لقائمة الأبناء، يجب دائمًا إضافة Get Records مخصص عند النزول للأبناء)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Lookup Relationship]] | Defines the Child→Parent link that makes traversal possible |
| [[Master-Detail]] | Same traversal logic, plus enables [[Rollup Summary Field]] going the other way |
| [[SOQL]] | The query language behind both traversal directions |
| [[Flow]] | Get Records + Loop is how Parent→Child traversal is built visually |
| [[Junction Object]] | Traversed in Flows using BOTH directions at once (e.g. Opportunity Product) |

## ❓ Rule to Remember
> **Child → Parent** = one record, direct dot access, no loop (`{!Record.Parent.Field}`)
> **Parent → Child** = many records, needs a separate Get Records filtered by the parent's ID, then a Loop
> This single rule explains almost every multi-step "Get Records" chain you'll ever build in Flow.

---
### 🔗 Related Notes
[[Lookup Relationship]] | [[Master-Detail]] | [[Junction Object]] | [[SOQL]] | [[Flow]] | [[Opportunity]] | [[Opportunity Product]] | [[Price Book Entry]]
