---
tags: [salesforce, platform, concept]
aliases: [sObject, Custom Object, Standard Object]
---

# 🗂️ Objects

## 📌 Definition
**Object** = a **table** that stores a specific type of data in Salesforce.
(جدول يخزن نوعًا معينًا من البيانات)

> Think of it like an Excel sheet:
> - The **Object** = the sheet name (e.g. "Accounts")
> - The **Fields** = the column headers (e.g. Name, Phone, Industry)
> - The **Records** = the rows (e.g. "Microsoft", "Apple")

## 🧠 Core Idea
Every piece of data you've studied so far — [[Lead]], [[Account]], [[Contact]], [[Opportunity]], [[Product]] — is an **Object**.
(كل ما درسناه سابقًا هو في الأصل Object)

Objects are the **containers**. Everything else (Fields, Relationships, Flows, Validation Rules) is built **on top of** an Object.

## 🧾 Two Types of Objects
| Type | Description |
|---|---|
| **Standard Object** | Comes built-in with Salesforce (Account, Contact, Opportunity, Lead, Case...) |
| **Custom Object** | Created by an Admin for a specific business need (e.g. `Invoice__c`, `Warranty__c`) |

> Custom Objects always end with `__c` in their API name.
(الـ Custom Objects تنتهي دائمًا بـ __c)

## 💡 Example
A company that rents cars might need a custom object:
```
Object: Car_Rental__c
Fields: Car Model, Rental Date, Return Date, Customer
```
This doesn't exist by default in Salesforce — the Admin creates it.
(هذا لا يوجد افتراضيًا، الـ Admin هو من ينشئه)

## 🔗 What Sits On Top of an Object
| Concept | Relation to Object |
|---|---|
| [[Fields]] | Define what data an Object stores (columns) |
| [[Lookup Relationship]] / [[Master-Detail]] | Connect one Object to another |
| [[Validation Rules]] | Control what data can be saved into the Object |
| [[Flow]] | Automate actions based on an Object's data |
| [[Reports]] / [[Dashboards]] | Read and visualize data from Objects |

## ❓ Rule to Remember
> Object = the table (الجدول)
> Field = the column (العمود)
> Record = the row (السطر)
>
> Standard Object = built by Salesforce
> Custom Object = built by you, ends with `__c`

---
### 🔗 Related Notes
[[Fields]] | [[Lookup Relationship]] | [[Master-Detail]] | [[Account]] | [[Opportunity]]
