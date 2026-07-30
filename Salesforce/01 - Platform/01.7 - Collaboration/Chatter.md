---
tags: [salesforce, platform, concept, collaboration]
aliases: [Chatter Feed]
---

# 💬 Chatter

## 📌 Definition
**Chatter** = Salesforce's built-in social collaboration tool — like an internal social feed attached to records, users, and groups.
(أداة التواصل الداخلية المدمجة في Salesforce، أشبه بفيسبوك داخلي مرتبط بالسجلات والمستخدمين والمجموعات)

> Lets employees **comment, share updates, and tag each other** directly on Salesforce records.
(يسمح للموظفين بالتعليق ومشاركة التحديثات والإشارة لبعضهم مباشرة على السجلات)

## 🧠 Core Idea
Chatter answers: **"How do people on the team talk about THIS specific record, without leaving Salesforce or losing context?"**
(كيف يتحدث الفريق عن هذا السجل بالتحديد، دون مغادرة Salesforce أو فقدان السياق؟)

## 🧾 What Chatter Provides
| Feature | Example |
|---|---|
| **Record Feed** | A comment thread directly on an [[Opportunity]] or [[Account]] record |
| **@Mentions** | Tag a colleague: `"@Sara can you review this discount?"` |
| **Following** | Get notified whenever a followed record changes |
| **Groups** | Create a "Sales Team Morocco" group for team-wide discussions |
| **Files** | Attach and share documents directly in the feed |

## 💡 Real Example
```
Opportunity: "CRM Project" ($50,000)

Chatter Feed:
Ahmed: "Client asked for a 15% discount, thoughts?"
   @Manager: "Approved, go ahead."
Sara: "I've updated the Quote, see attached file."
```
Instead of emailing back and forth, the entire conversation happens
**directly on the record itself**, visible to anyone following it.
(بدل تبادل الإيميلات، تحدث المحادثة كاملة مباشرة على السجل نفسه)

## 🔗 Where It Connects to What We've Studied
- Following an [[Opportunity]] → get notified when its Stage changes to "Closed Won" (often paired with [[Flow]] notifications)
- Commenting on a [[Case]] (Service Cloud) → support agents collaborate on a tricky customer issue
- Tagging a colleague on an [[Account]] → ask a quick question without opening email

## ⚖️ Chatter vs Email/Slack
| | Chatter | External Email/Slack |
|---|---|---|
| Context | Directly attached to the Salesforce record | Separate from the record, easy to lose context |
| Visibility | Anyone with access to the record can see the history | Scattered across inboxes/channels |
| Best for | Record-specific discussions | General company-wide communication |

(ميزة Chatter الأساسية أن النقاش يبقى ملتصقًا بالسجل، فلا يضيع السياق)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Objects]] | Chatter feeds can be enabled per Object |
| [[Security Model]] | A user can only see/comment on a record's feed if they have access to that record |
| [[Flow]] | Flows can post automated Chatter updates (e.g. "Deal moved to Negotiation") |

## ❓ Rule to Remember
> Chatter = **internal social feed attached to records** (شبكة تواصل داخلية مرتبطة بالسجلات)
> Comments, @mentions, following, groups, and file sharing — all without leaving Salesforce.
> Keeps team discussions attached to the exact record they're about, unlike email/Slack.

---
### 🔗 Related Notes
[[Objects]] | [[Security Model]] | [[Flow]] | [[Opportunity]] | [[Account]]
