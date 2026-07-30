---
tags: [salesforce, platform, concept]
aliases: [Record Type]
---

# 🗃️ Record Types

## 📌 Definition
**Record Type** = a way to give **different Picklist values, Page Layouts, and Business Processes** to different kinds of records within the **same** [[Objects|Object]].
(طريقة لإعطاء قيم Picklist وPage Layouts مختلفة لأنواع مختلفة من السجلات داخل نفس الـ Object)

> Same Object, same Fields — but different **flavors** depending on the situation.
(نفس الـ Object، نفس الحقول، لكن بنكهات مختلفة حسب الحالة)

## 🧠 Core Idea
A Record Type answers: **"This record is technically the same Object, but it behaves differently — how do I show the right options for the right context?"**
(نفس الـ Object تقنيًا، لكنه يتصرف بشكل مختلف، كيف أعرض الخيارات الصحيحة حسب السياق؟)

## 💡 Real Example
The [[Opportunity]] Object could have two Record Types:
| Record Type | Stage Picklist Values Shown | Page Layout |
|---|---|---|
| **New Business** | Prospecting → Qualification → Proposal → Negotiation → Closed Won/Lost | Full layout with lead source |
| **Renewal** | Renewal Sent → Renewal Negotiation → Renewed / Not Renewed | Simplified layout, no lead source |

Same Object (`Opportunity`), same underlying table — but a Sales Rep working
on a **New Business** deal sees completely different Stage options than one
working on a **Renewal**.
(نفس الـ Object، لكن خيارات الـ Stage مختلفة تمامًا حسب نوع السجل)

## 🧾 What a Record Type Can Control
| Controls | Example |
|---|---|
| Picklist Values | Different Stage options for New Business vs Renewal |
| Page Layout | Different fields shown/hidden per Record Type |
| Business Process | Different approval or sales process per type |
| Default assignment | New records can auto-assign a specific Record Type based on the creating Profile |

## ⚖️ Record Type vs Profile — Who Controls What?
| | [[Profiles]] | Record Type |
|---|---|---|
| Controls | Which Record Types a user **can access** | Which Picklist values/Layout **appear** for that type |
| Question answered | "Can this user use the Renewal record type?" | "What does the Renewal record type actually look like?" |

(الـ Profile يحدد من يستطيع استخدام نوع سجل معين، والـ Record Type يحدد شكل ومحتوى هذا النوع)

## 💡 Another Common Example
The [[Account]] Object might have:
| Record Type | Purpose |
|---|---|
| **Customer** | Standard fields for paying customers |
| **Partner** | Extra fields for partner-specific info (commission %, territory) |
| **Prospect** | Simplified layout before they become a real customer |

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Objects]] | A Record Type always belongs to one specific Object |
| [[Fields]] | Record Types don't create new Fields — they control which Picklist values of an existing field are shown |
| [[Profiles]] | Profiles determine which Record Types a user is allowed to use |
| Page Layouts | Each Record Type can be linked to a different Page Layout |

## ❓ Rule to Remember
> Record Type = **different flavors of the same Object** (نكهات مختلفة لنفس الـ Object)
> Controls which Picklist values and which Page Layout appear.
> Does NOT create new fields — only customizes how existing fields/values are shown.
> Access to a Record Type is granted through the user's [[Profiles|Profile]].

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Profiles]] | [[Opportunity]] | [[Account]]
