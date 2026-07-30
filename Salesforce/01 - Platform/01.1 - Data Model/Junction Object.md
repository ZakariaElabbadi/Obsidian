---
tags: [salesforce, platform, concept, relationship]
aliases: [Junction Object, Many-to-Many Relationship]
---

# 🔀 Junction Object

## 📌 Definition
**Junction Object** = a custom Object placed **between two Objects** to create a **Many-to-Many** relationship.
(Object مخصص يوضع بين Objectين لإنشاء علاقة "كثير إلى كثير")

> Salesforce doesn't support Many-to-Many directly — a Junction Object is
> the standard technique to simulate it, using **two** [[Master-Detail]]
> (or Lookup) relationships.
(Salesforce لا يدعم علاقة كثير-إلى-كثير مباشرة، والحل هو Junction Object)

## 🧠 Core Idea
A Junction Object answers: **"One record on Side A can relate to MANY records on Side B, and one record on Side B can relate to MANY records on Side A — how do we model that?"**
(سجل واحد من جهة A يمكن أن يرتبط بعدة سجلات من جهة B، والعكس صحيح، كيف نمذجة ذلك؟)

## 💡 You Already Know One! 🎯
Remember [[Opportunity Product]]?
```
Opportunity  ──────┐
                    ├──► Opportunity Product  ◄──── this IS a Junction Object
Product      ──────┘
```
- One [[Opportunity]] can have **many** [[Product]]s (Generator, Battery, Warranty...)
- One [[Product]] can appear in **many** different Opportunities

Neither a direct Lookup nor a single Master-Detail could handle this — so
Salesforce uses **Opportunity Product** as the Junction Object in between.
(لا يمكن حل هذا بعلاقة مباشرة، لذلك يُستخدم Opportunity Product كـ Junction Object)

```
Opportunity (Master)
     │
     ▼ Master-Detail #1
Opportunity Product (Junction)
     ▲
     │ Master-Detail #2 (via Price Book Entry → Product)
Product
```

## 🧾 How a Junction Object Is Built
| Requirement | Details |
|---|---|
| Two Master-Detail relationships | One to each "parent" Object |
| (Sometimes Lookup instead) | Used when full dependency isn't needed |
| Extra fields allowed | Store info specific to the *pairing* itself (e.g. Quantity, Discount) |

This is exactly why [[Opportunity Product]] can hold `Quantity`, `Unit Price`,
and `Discount` — those values only make sense for **that specific pairing**
of an Opportunity with a Product, not for the Opportunity or Product alone.
(هذه القيم منطقية فقط لهذا الاقتران المحدد بين الصفقة والمنتج)

## 🧾 Another Classic Example
```
Student  ──────┐
                ├──► Enrollment (Junction Object)
Course   ──────┘
```
- One Student can enroll in **many** Courses
- One Course can have **many** Students
- The Junction Object `Enrollment` can also store `Grade`, `Enrollment Date`
  — data specific to that particular student-course pairing.

## ⚖️ Junction Object vs Direct Relationships
| | Direct Lookup/Master-Detail | Junction Object |
|---|---|---|
| Relationship type | One-to-Many only | Many-to-Many |
| Extra pairing-specific data? | ❌ No | ✅ Yes (e.g. Quantity, Grade) |
| Requires a middle Object? | ❌ No | ✅ Yes, always |

(العلاقة المباشرة تدعم فقط واحد-إلى-كثير، بينما Junction Object يحل كثير-إلى-كثير)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Master-Detail]] | A Junction Object is usually built using TWO Master-Detail relationships |
| [[Objects]] | The Junction Object is a real, standalone custom Object |
| [[Fields]] | Extra fields on the Junction store data specific to that one pairing |
| [[Opportunity Product]] | The exact Junction Object example you've already studied |

## ❓ Rule to Remember
> Junction Object = the fix for **Many-to-Many** relationships (حل علاقة كثير-إلى-كثير)
> Built from TWO Master-Detail relationships, one to each side.
> Can hold extra fields specific to that pairing (e.g. Quantity, Discount, Grade).
> [[Opportunity Product]] is the perfect real-world example already covered in Sales Cloud.

---
### 🔗 Related Notes
[[Master-Detail]] | [[Lookup Relationship]] | [[Objects]] | [[Opportunity]] | [[Product]] | [[Opportunity Product]]
