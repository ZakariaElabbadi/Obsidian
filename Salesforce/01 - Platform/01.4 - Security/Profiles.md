---
tags: [salesforce, platform, concept, security]
aliases: [Profile]
---

# 🪪 Profiles

## 📌 Definition
**Profile** = a set of permissions that controls **what a user can do** in Salesforce.
(مجموعة من الصلاحيات تحدد ما يمكن للمستخدم فعله)

> Every user has **exactly one** Profile — no more, no less.
(كل مستخدم لديه Profile واحد فقط، لا أكثر)

## 🧠 Core Idea
A Profile answers questions like:
- Which [[Objects]] can this user see? (Account, Opportunity, Case...)
- Can they Create / Read / Edit / Delete records?
- Which fields can they view or edit?
- Which apps/tabs can they access?
- What are their login hours / IP restrictions?

## 🧾 What a Profile Controls
| Permission Type | Example |
|---|---|
| Object Permissions | Can the user Create/Read/Edit/Delete [[Opportunity]] records? |
| Field-Level Security | Can they see the "Discount" field on Opportunity Product? |
| App/Tab Access | Can they open the Service Cloud app? |
| System Permissions | Can they export reports, manage users, modify all data? |
| Login Restrictions | Login hours, IP ranges |

## 💡 Real Example
| Profile | Access |
|---|---|
| Sales Rep | Can create/edit [[Lead]], [[Opportunity]] — cannot delete Accounts |
| Sales Manager | Full access to Sales Cloud objects + reports |
| System Administrator | Full access to everything in the org |
| Customer Support | Can access [[Case]] — no access to Opportunity |

(كل Profile يحدد الحد الأقصى لما يمكن للمستخدم رؤيته أو فعله)

## ⚖️ Profile vs Permission Set
| | Profile | [[Permission Sets]] |
|---|---|---|
| How many per user? | Exactly **one** | **Many** (stacked on top) |
| Purpose | Baseline access (الصلاحيات الأساسية) | Extra, specific access (صلاحيات إضافية) |
| Use case | "This is a Sales Rep" | "This specific Sales Rep also needs to see Reports" |

(الفرق الأهم: Profile واحد إجباري، لكن Permission Sets متعددة واختيارية لإضافة صلاحيات إضافية)

## 💡 Example Combining Both
```
User: Ahmed
Profile: Sales Rep          → baseline access to Lead, Opportunity
+ Permission Set: "Report Access" → extra access to Reports & Dashboards
```
Instead of creating a brand-new Profile just for reporting access, the Admin
adds a **Permission Set** on top of the existing Profile.
(بدل إنشاء Profile جديد، يضيف الـ Admin Permission Set فوق الـ Profile الحالي)

## ❓ Rule to Remember
> Profile = the **baseline** permission set — every user has exactly one.
> Controls Object access, Field-Level Security, App access, and login restrictions.
> For extra/specific access without changing the whole Profile → use [[Permission Sets]].

---
### 🔗 Related Notes
[[Permission Sets]] | [[Objects]] | [[Fields]] | [[Reports]]
