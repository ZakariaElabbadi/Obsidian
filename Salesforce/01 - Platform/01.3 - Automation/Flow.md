---
tags: [salesforce, platform, concept, automation]
aliases: [Salesforce Flow, Flow Builder]
---

# ⚙️ Flow

## 📌 Definition
**Flow** = Salesforce's automation tool — it performs actions automatically based on data changes or user input, without writing code.
(أداة الأتمتة في Salesforce، تنفذ إجراءات تلقائيًا بدون كتابة كود)

> Think of it as: *"When X happens, automatically do Y."*
(عندما يحدث X، نفّذ Y تلقائيًا)

## 🧠 Core Idea
A Flow is built from simple building blocks:
```
Trigger (what starts it)
     │
     ▼
Get Records   → read data from an Object
     │
     ▼
Decision      → check a condition
     │
     ▼
Create / Update Records → change data
     │
     ▼
Action (Email, Task, etc.)
```

## 🧾 Types of Flows
| Type | When It Runs |
|---|---|
| **Record-Triggered Flow** | Automatically, when a record is created/updated/deleted |
| **Screen Flow** | Guides a user through steps with a UI (forms, buttons) |
| **Scheduled Flow** | Runs at a set time (daily, weekly...) |
| **Autolaunched Flow** | Triggered by another process (e.g. another Flow, Apex) |

## 💡 The Exact Example We Studied
Remember this Flow from the [[Opportunity Product]] lesson:
```
Get Price Book       → Which price list are we using?
     ↓
Get Product           → Which product are we selling?
     ↓
Get Price Book Entry   → What's the price of this product in this list?
     ↓
Create Opportunity Product → Add the product (with qty & price) to the deal
```
This entire sequence is a **Flow** — it reads data from multiple [[Objects]]
in a logical order, then creates a new record automatically.
(كل هذا التسلسل هو Flow واحد يقرأ البيانات وينشئ سجلًا جديدًا تلقائيًا)

## 🔗 Common Elements Inside a Flow
| Element | Purpose |
|---|---|
| Get Records | Fetch existing data from an Object (e.g. Get Product) |
| Create Records | Insert a new record (e.g. Create Opportunity Product) |
| Update Records | Modify an existing record |
| Decision | Branch logic — IF/ELSE conditions |
| Loop | Repeat an action for multiple records |
| Assignment | Store a value in a variable for later use |

## ⚖️ Flow vs Validation Rule
| | [[Validation Rules]] | Flow |
|---|---|---|
| Purpose | Blocks bad data from saving | Automates actions/processes |
| Can create records? | ❌ No | ✅ Yes |
| Can send emails? | ❌ No | ✅ Yes |
| Complexity | Simple TRUE/FALSE check | Can be a full multi-step process |

## 💡 Real Example
```
When Opportunity.Stage = "Closed Won"
     │
     ▼ Flow triggers:
     ├── Send confirmation Email
     ├── Create a Case for implementation
     ├── Create a Task for the support team
     └── Create an Order
```
(عندما تصبح Stage = Closed Won، ينفذ الـ Flow كل هذه الإجراءات تلقائيًا)

## ❓ Rule to Remember
> Flow = **"When this happens, do that automatically"** (عندما يحدث هذا، نفّذ ذلك تلقائيًا)
> Reads data with **Get Records**, decides with **Decision**, acts with **Create/Update Records**.
> Always follow the logical dependency order — you can't create a record before fetching the data it depends on.

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Validation Rules]] | [[Opportunity]] | [[Opportunity Product]] | [[Price Book Entry]]
