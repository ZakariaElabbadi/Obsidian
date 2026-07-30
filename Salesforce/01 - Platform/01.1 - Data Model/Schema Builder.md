---
tags: [salesforce, platform, concept, tool]
aliases: [Schema Builder Tool]
---

# 🧭 Schema Builder

## 📌 Definition
**Schema Builder** = a visual tool in Salesforce that shows all [[Objects]], their [[Fields]], and the [[Lookup Relationship|Lookup]]/[[Master-Detail]] relationships between them — as an interactive diagram.
(أداة بصرية تعرض كل الـ Objects والحقول والعلاقات بينها على شكل مخطط تفاعلي)

> It's essentially a **live, visual map** of your entire data model — exactly
> like the diagrams we've been drawing by hand in this vault, but generated
> automatically by Salesforce itself.
(خريطة بصرية حية لكل نموذج البيانات، تمامًا مثل المخططات التي رسمناها يدويًا، لكنها تُولّد تلقائيًا)

## 🧠 Core Idea
Schema Builder answers: **"How does everything in my org connect together, visually, without me drawing it myself?"**
(كيف يترابط كل شيء في الـ Org بصريًا، دون أن أرسمه بنفسي؟)

## 🧾 What You Can Do in Schema Builder
| Action | Description |
|---|---|
| **View relationships** | See every Lookup and Master-Detail line connecting Objects |
| **View fields** | Expand any Object to see its full list of Fields and types |
| **Create new Objects** | Drag-and-drop a new Custom Object directly onto the canvas |
| **Create new Fields** | Add fields to existing Objects visually |
| **Create relationships** | Draw a new Lookup or Master-Detail connection between two Objects |

## 💡 Real Example
Opening Schema Builder for the Objects we've studied would show something
very close to our own diagram:
```
[Lead] ──Convert──> [Account] ──Master-Detail──> [Opportunity]
                        │                              │
                     [Contact]                [Opportunity Product] ──> [Price Book Entry]
                                                                              │
                                                                    ┌─────────┴─────────┐
                                                                [Product]          [Price Book]
```
Every arrow you see in Schema Builder corresponds to a real
[[Lookup Relationship]] or [[Master-Detail]] configured in the org.
(كل سهم في Schema Builder يمثل علاقة حقيقية مُعدة في الـ Org)

## ⚖️ Schema Builder vs Object Manager
| | Object Manager | Schema Builder |
|---|---|---|
| View | List-based, one Object at a time | Visual diagram, all Objects at once |
| Best for | Detailed field-by-field setup | Understanding the big picture / relationships |
| Editing | Full control over every setting | Quick visual creation, some settings still need Object Manager |

(Object Manager للتفاصيل الدقيقة، بينما Schema Builder لرؤية الصورة الكاملة والعلاقات)

## ⚠️ Why Admins Use It
- Quickly explain the data model to a new team member (تشرح نموذج البيانات لعضو جديد بسرعة)
- Spot missing or incorrect relationships between Objects
- Plan a new Custom Object visually before creating it formally

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Objects]] | Schema Builder visualizes every Object in the org |
| [[Fields]] | Each Object node can expand to show its Fields |
| [[Lookup Relationship]] | Shown as connecting lines between Objects |
| [[Master-Detail]] | Shown with a distinct line style, indicating dependency |
| [[Junction Object]] | Easy to spot visually — it's the Object with two Master-Detail lines going to different parents |

## ❓ Rule to Remember
> Schema Builder = **visual, interactive map of the data model** (خريطة بصرية تفاعلية لنموذج البيانات)
> Shows Objects, Fields, and every Lookup/Master-Detail relationship at once.
> Great for understanding the big picture — Object Manager is still needed for fine-grained setup.

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Lookup Relationship]] | [[Master-Detail]] | [[Junction Object]]
