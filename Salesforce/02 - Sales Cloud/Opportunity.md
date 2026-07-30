---
tags: [salesforce, sales-cloud, object]
aliases: [Sales Deal, Deal]
---

# 💰 Opportunity

## 📌 Definition
**Opportunity** = a **Sales Deal** — a real chance of selling something.
(فرصة بيع، وليست عملية بيع مكتملة)

> Opportunity answers questions like:
> - How much is this deal worth?
> - What stage is it in?
> - When will it close?
> - Did we win it or lose it?

## 🧠 Core Idea
An [[Account]] only tells us **who** the company is.
It does NOT tell us:
- ❌ How much they're buying
- ❌ Whether we won or lost the deal
- ❌ When it will close

All of that lives inside the **Opportunity**.
(كل هذا يوجد داخل Opportunity، وليس داخل Account)

## 🔄 Where Does It Come From?
An Opportunity can be created:
- When a [[Lead]] is **Converted** (if there's real buying intent)
- Or manually, when an existing Account starts a new deal

```
Lead
 │
 │ Convert
 ▼
Opportunity   ← the Deal (الصفقة)
```

## 🔗 Relationship to Other Objects
| Relationship | Description |
|---|---|
| Account → Opportunity | One Account can have **many** Opportunities (multiple deals over time) |
| Contact → Opportunity | The Contact is the person we negotiate the deal with |

```
Microsoft (Account)
   │
   ├── Ahmed (Contact)
   │
   ├── Opportunity: CRM Project      ($50,000)
   ├── Opportunity: Service Cloud    ($20,000)
   └── Opportunity: AI Project       ($80,000)
```

## 🧾 Key Fields
| Field | Meaning |
|---|---|
| Name | Deal name (اسم الصفقة) |
| Amount | Deal value (قيمة الصفقة) |
| Stage | Current sales stage (مرحلة البيع) |
| Close Date | Expected closing date (التاريخ المتوقع للإغلاق) |
| Account | Linked company (الشركة المرتبطة) |

## 📊 Sales Pipeline (Stages)
```
Prospecting
    │
    ▼
Qualification
    │
    ▼
Proposal
    │
    ▼
Negotiation
    │
    ▼
Closed Won  🎉      or      Closed Lost  😞
```

| Stage | Meaning |
|---|---|
| Prospecting | Customer showed interest, first contact started (العميل أبدى اهتمامًا) |
| Qualification | Confirmed the customer is a good fit with a budget (تأكدنا أنه عميل مناسب) |
| Proposal | We sent a price quote (أرسلنا عرض السعر) |
| Negotiation | Negotiating price and terms (نتفاوض على السعر والشروط) |
| Closed Won | 🎉 We won the deal, customer bought (ربحنا الصفقة) |
| Closed Lost | 😞 Customer bought from a competitor (خسرنا الصفقة) |

## ⚠️ Why Can One Account Have Many Opportunities?
Because a company can buy from us more than once, and each purchase is a **separate deal**.
(كل صفقة جديدة = Opportunity جديدة، حتى لو كانت نفس الشركة)

Example:
> Microsoft bought CRM this year.
> Six months later, they want a Service Cloud system too.
> - ❌ Not the same deal
> - ✅ We create a **new Opportunity**

## ⚙️ Using Opportunity in Flows
When **Stage = Closed Won**, a Flow can automatically:
- Send a confirmation Email
- Create a Case for implementation
- Create a Task for the support team
- Create an Order (covered later)

(عندما تصبح Stage = Closed Won، يمكن للـ Flow أن ينفذ هذه الإجراءات تلقائيًا)

## 💡 Real Example
> Microsoft wants to buy a CRM system worth $50,000.

```
Opportunity
Name: CRM Project
Amount: $50,000
Stage: Proposal
Close Date: 31/12/2026
```

> Two weeks later, the customer agrees.
> We change Stage → **Closed Won**
> A Flow can now trigger automatically. 🎉

## ❓ Rule to Remember
> Account = the Company (لا يتغير)
> Opportunity = each Deal (يتغير مع كل صفقة جديدة)
> One Account → Many Opportunities, each with its own Amount and Stage.

---
### 🔗 Related Notes
[[Lead]] | [[Account]] | [[Contact]]
