---
tags: [salesforce, platform, concept]
aliases: [Salesforce Object Query Language]
---

# 🔎 SOQL

## 📌 Definition
**SOQL** (Salesforce Object Query Language) = the query language used to **retrieve records** from Salesforce [[Objects]].
(لغة الاستعلام المستخدمة لجلب السجلات من الـ Objects في Salesforce)

> It looks similar to SQL, but it's designed specifically to query Salesforce data
> and understand relationships between Objects.
(تشبه SQL، لكنها مصممة خصيصًا للاستعلام عن بيانات Salesforce والعلاقات بين الـ Objects)

## 🧠 Core Idea
SOQL answers: **"Give me exactly these records, with these fields, matching this condition."**
(أعطني هذه السجلات بالضبط، بهذه الحقول، وبهذا الشرط)

## 🧾 Basic Structure
```sql
SELECT Field1, Field2
FROM ObjectName
WHERE Condition
```

## 💡 Real Example
```sql
SELECT Name, Amount, StageName
FROM Opportunity
WHERE StageName = 'Closed Won'
AND CloseDate = THIS_MONTH
```
This retrieves the Name, Amount, and Stage of every [[Opportunity]] that was
**Closed Won this month** — the exact data a Sales Manager might want for a Report.
(هذا الاستعلام يجلب كل الصفقات التي رُبحت هذا الشهر)

## 🔗 Querying Relationships (Parent → Child and Child → Parent)
SOQL can traverse [[Lookup Relationship]] and [[Master-Detail]] connections directly.

**Child-to-Parent** (dot notation):
```sql
SELECT Name, Account.Name
FROM Contact
```
→ Gets each [[Contact]]'s name **and** their related [[Account]]'s name in one query.

**Parent-to-Child** (subquery):
```sql
SELECT Name, (SELECT Name, Amount FROM Opportunities)
FROM Account
```
→ Gets each [[Account]] along with **all its related Opportunities**.

## ⚖️ Where SOQL Is Used
| Context | Purpose |
|---|---|
| [[Flow]] | "Get Records" elements run SOQL behind the scenes |
| Apex Code | Developers write SOQL directly to fetch data |
| Reports | Built visually, but powered by SOQL logic underneath |

(عندما تستخدم "Get Records" داخل Flow، فأنت فعليًا تُشغّل SOQL خلف الكواليس)

## ⚠️ SOQL vs SQL — Key Difference
| | SQL | SOQL |
|---|---|---|
| Works on | Any relational database | Only Salesforce Objects |
| JOIN keyword | ✅ Yes | ❌ No — uses relationship dot-notation/subqueries instead |
| SELECT * | ✅ Allowed | ❌ Not allowed — must name each field explicitly |

(لا يوجد JOIN في SOQL، ولا يمكن استخدام * لجلب كل الحقول، يجب تسميتها بشكل صريح)

## ❓ Rule to Remember
> SOQL = **the query language to fetch Salesforce data**
> `SELECT fields FROM Object WHERE condition`
> Can traverse relationships: Child→Parent with dot notation, Parent→Child with subqueries.
> Powers "Get Records" in [[Flow]] behind the scenes.

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Flow]] | [[Lookup Relationship]] | [[Master-Detail]] | [[Reports]]
