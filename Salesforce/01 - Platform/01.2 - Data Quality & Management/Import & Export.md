---
tags: [salesforce, platform, concept, data-management]
aliases: [Data Import, Data Export, Data Loader]
---

# 📤 Import & Export

## 📌 Definition
**Import** = bringing data **into** Salesforce (e.g. from an Excel/CSV file).
**Export** = taking data **out of** Salesforce (e.g. for backup or analysis elsewhere).
(الاستيراد = إدخال بيانات إلى Salesforce، التصدير = إخراج بيانات منه)

> These are the main ways bulk data moves in and out of [[Objects]] without manual, one-by-one data entry.
(الطريقة الرئيسية لنقل كميات كبيرة من البيانات دون إدخالها يدويًا واحدة تلو الأخرى)

## 🧠 Core Idea
Import/Export answers: **"I have (or need) hundreds/thousands of records — how do I move them efficiently?"**
(لدي أو أحتاج مئات أو آلاف السجلات، كيف أنقلها بكفاءة؟)

## 🧾 Common Import Tools
| Tool | Best For |
|---|---|
| **Data Import Wizard** | Simple imports (Accounts, Contacts, Leads, Custom Objects) — up to 50,000 records, easy UI |
| **Data Loader** | Large volumes (millions of records), all Objects, supports insert/update/upsert/delete |
| **Import via Flow/Apex** | Automated, ongoing imports as part of a business process |

## 💡 Real Example — Import
```
A company has 5,000 old customer records in an Excel file.

Using Data Loader:
1. Map Excel columns → Salesforce Fields (Name, Phone, Industry...)
2. Choose target Object → Account
3. Run the import
4. 5,000 new Account records are created in minutes
```
(بدل إدخال 5000 سجل يدويًا، يتم استيرادها دفعة واحدة)

## 💡 Real Example — Export
```
A Sales Manager needs all Closed Won Opportunities from last year
for a financial audit outside Salesforce.

Using Data Export / Reports export:
1. Build a Report filtered by Stage = Closed Won, Year = last year
2. Export to Excel/CSV
3. Share the file with the finance team
```
(تصدير بيانات الصفقات المربوحة لتحليلها خارج Salesforce)

## ⚠️ Upsert — A Key Concept
**Upsert** = Update if the record already exists, Insert if it doesn't — in a single operation.
(تحديث السجل إن كان موجودًا، أو إنشاؤه إن لم يكن موجودًا، في عملية واحدة)

This relies on a unique identifier, such as an **External ID** field, to match
incoming data with existing Salesforce records.
(يعتمد على معرّف فريد مثل External ID لمطابقة البيانات القادمة مع السجلات الموجودة)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Objects]] | Import/Export always targets a specific Object |
| [[Fields]] | Columns in the file must be mapped to specific Fields |
| [[Validation Rules]] | Still apply during import — bad data can be rejected |
| [[Reports]] | The most common way to export data out of Salesforce |

## ❓ Rule to Remember
> Import = data **into** Salesforce (bulk, not manual)
> Export = data **out of** Salesforce (backup, analysis, sharing)
> Upsert = smart import — update if it exists, insert if it doesn't
> Validation Rules still apply during import — bulk doesn't mean "no rules."

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Validation Rules]] | [[Reports]] | [[SOQL]]
