---
tags: [salesforce, platform, concept, security]
aliases: [Permission Set]
---

# 🎟️ Permission Sets

## 📌 Definition
**Permission Set** = a collection of **extra permissions** given to a user **on top of** their [[Profiles|Profile]].
(مجموعة صلاحيات إضافية تُمنح للمستخدم فوق الـ Profile الخاص به)

> A user can have **zero, one, or many** Permission Sets — unlike Profile, which is always exactly one.
(يمكن أن يكون لدى المستخدم صفر أو واحد أو عدة Permission Sets)

## 🧠 Core Idea
Permission Sets answer: **"This user's Profile is mostly right, but they need a bit more access — how do we add just that, without changing everyone else?"**
(الـ Profile مناسب تقريبًا، لكن هذا المستخدم يحتاج صلاحية إضافية فقط)

## 💡 Real Example
```
User: Ahmed
Profile: Sales Rep → standard access to Lead, Opportunity

Problem: Ahmed also needs to export Reports,
         but other Sales Reps should NOT have this access.

Solution: Create a Permission Set "Report Export Access"
          and assign it ONLY to Ahmed.
```
(بدل تعديل الـ Profile بالكامل، أو إنشاء Profile جديد فقط لأجل أحمد، نضيف Permission Set خاص به)

## ⚖️ Why Not Just Edit the Profile?
| Approach | Problem |
|---|---|
| Edit the shared Profile | Affects **every** Sales Rep, not just Ahmed |
| Create a brand-new Profile | Too heavy for just one small extra permission |
| ✅ Use a Permission Set | Adds access to Ahmed only, keeps everyone else unchanged |

(تعديل الـ Profile يؤثر على الجميع، بينما Permission Set يستهدف مستخدمًا أو مجموعة محددة فقط)

## 🧾 What a Permission Set Can Grant
| Type | Example |
|---|---|
| Object Permissions | Extra access to a specific Object (e.g. Reports) |
| Field-Level Security | View/Edit a specific field not in their Profile |
| App Access | Access to an extra app or tab |
| System Permissions | "Export Reports", "Manage Public List Views" |

## ⚖️ Profile vs Permission Set — Quick Comparison
| | [[Profiles|Profile]] | Permission Set |
|---|---|---|
| How many per user | Exactly one | Zero, one, or many |
| Purpose | Baseline access | Additional, targeted access |
| Removes access? | Defines the ceiling | Only **adds**, never removes |
| Best for | "What kind of user is this?" | "This user needs one extra thing" |

## 💡 Analogy
> Profile = your job title's default badge (e.g. "Sales Rep" badge opens standard doors).
> Permission Set = an extra keycard clipped on top, opening one specific extra door
> (like the Reports room) — without needing a whole new badge.
(الـ Profile كأنه بطاقة الوظيفة الأساسية، والـ Permission Set كأنه مفتاح إضافي لباب واحد فقط)

## ❓ Rule to Remember
> Permission Set = **additive only** (يضيف فقط، لا يزيل صلاحيات)
> Used when a specific user (or group) needs a bit more than their Profile gives them.
> Multiple Permission Sets can be stacked on the same user.

---
### 🔗 Related Notes
[[Profiles]] | [[Objects]] | [[Fields]] | [[Reports]]
