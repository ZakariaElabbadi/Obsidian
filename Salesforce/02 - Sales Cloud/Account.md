---
tags: [salesforce, sales-cloud, object]
aliases: [Company, Customer Company]
---

# 🏢 Account

## 📌 Definition
**Account** = the **Company** or **Organization** we do business with.
(الشركة أو العميل)

> Account answers one question only:
> **"Who is the company?"**
> Nothing more.

## 🧠 Core Idea
An Account does **not** tell us:
- ❌ How much they will buy
- ❌ Whether they will buy at all
- ❌ Who inside the company we talk to

It only tells us:
- ✅ This company exists as a customer/prospect record
(Account يخبرنا فقط أن الشركة عميل لدينا)

## 🔄 Where Does It Come From?
An Account is usually created when a [[Lead]] is **Converted**.

```
Lead
 │
 │ Convert
 ▼
Account   ← the Company (الشركة)
```

## 🔗 Relationship to Other Objects
| Relationship | Description |
|---|---|
| Account → Contact | One Account can have **many** Contacts (people who work there / الأشخاص داخل الشركة) |
| Account → Opportunity | One Account can have **many** Opportunities (deals / صفقات متعددة) |

```
Account (Microsoft)
   │
   ├── Contact: Ahmed
   ├── Contact: Saad
   │
   ├── Opportunity: CRM Project
   ├── Opportunity: Service Cloud
   └── Opportunity: AI Project
```

## ⚠️ Important Rule
**People change, deals change — but the Company usually stays the same.**
(الأشخاص يتغيرون، الصفقات تتغير، لكن الشركة تبقى غالبًا نفسها)

Example:
> Ali leaves the company, Saad joins.
> - ✅ We do NOT create a new Account
> - ✅ We create a new [[Contact]] for Saad
> - ✅ If there's a new deal, we create a new [[Opportunity]]

## 💰 Why Doesn't the Sale Amount Live Inside Account?
Because one Account can have **multiple deals**, each with a different value.

| Opportunity | Amount |
|---|---|
| CRM Project | $50,000 |
| Service Cloud | $20,000 |
| AI Project | $80,000 |

If we stored one single amount inside the Account, we wouldn't know **which deal** it refers to.
(لن نعرف أي صفقة يقصد)
That's why the Amount lives inside [[Opportunity]], not inside Account.

## 💡 Real Example
> Microsoft is our customer.
> We store it as one **Account** record.
> Over the years, Microsoft buys CRM, then Service Cloud, then AI tools —
> each one is a **separate Opportunity**, but they all belong to the **same Account**.

## ❓ Rule to Remember
> One Account → Many Contacts
> One Account → Many Opportunities
> (One Company, Many People, Many Deals)

---
### 🔗 Related Notes
[[Lead]] | [[Contact]] | [[Opportunity]]
