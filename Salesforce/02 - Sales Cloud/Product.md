---
tags: [salesforce, sales-cloud, object]
aliases: [Product2, Item, Merchandise]
---

# 📦 Product

## 📌 Definition
**Product** = the thing the company sells.
الشيء الذي تبيعه الشركة

> Examples:
> - Salesforce Enterprise License
> - Dell Laptop
> - iPhone 16
> - Generator 1500kW
> - Netflix Subscription

## 🧠 Core Idea
Product answers only one question:
**"What are we selling?"**

It does **NOT** answer:
- ❌ How much does it cost?
- ❌ Which company / customer bought it?
- ❌ Which deal is it part of?

كل هذه الأسئلة تُجاب من Objects أخرى، وليس من Product

## 🧾 Key Fields
| Field | Meaning |
|---|---|
| Product Name | Name of the product (اسم المنتج) |
| Product Code | Internal reference code (رمز المنتج) |
| Description | Product description (الوصف) |
| Active | Is it available for sale? (هل المنتج متاح للبيع؟) |

## 💰 Does Product Store the Price?
**❌ No.**
هذا من أكثر الأخطاء التي يقع فيها المبتدئون

Example — Dell Laptop:
| Country | Price |
|---|---|
| USA | $1,000 |
| Germany | $950 |
| Morocco | $900 |

Same product, different prices depending on:
- Country (الدولة)
- Customer type — regular / business / partner (نوع العميل)
- Promotions (العروض)

If the price lived inside Product, there could only be **one** price — which isn't enough.
لو وضعنا السعر داخل Product سيكون لدينا سعر واحد فقط، وهذا لا يكفي

👉 The price actually lives inside [[Price Book Entry]].

## 🔎 Simple Analogy
Think of a bookstore.
The **Product** is:
> "Learn Salesforce" book

But its price differs by location:
| Location | Price |
|---|---|
| Physical Store | $20 |
| Website | $18 |
| Book Fair | $15 |

Did the book change? ❌ No.
Only the **price** changed — and price is a separate concept from the product itself.
الكتاب لم يتغير، الذي تغير هو السعر فقط

## 🔗 Relationship to Other Objects
Product does **not** connect directly to [[Opportunity]].

```
Opportunity
     │
     ▼
Opportunity Product   ← links Opportunity to a Product
     │
     ▼
Price Book Entry       ← tells us the price
     ▲
     │
     ├──────────────┐
     ▼              ▼
  Product        Price Book
```

### Why not link Opportunity directly to Product?
Because one Opportunity can include **multiple products**:
- Laptop
- Mouse
- Keyboard

A single field on Opportunity can't point to three different Products at once.
(Opportunity لا تستطيع أن تشير إلى ثلاثة Products بحقل واحد)

That's why a separate object — [[Opportunity Product]] — exists to hold each line item.

## 💡 Real Example
A company that sells electric generators has these Products:
| Product |
|---|
| Generator 1500kW |
| Generator 2000kW |
| Generator 3000kW |

When a Flow searches for "1500" or "2000", it's actually searching for the matching **Product** record.
كان الـ Flow يبحث عن Product المناسب

## ⚙️ How Does an Admin Use It?
When a new Product is added (e.g. `Generator 5000kW`), a Flow could:
- Notify the sales team
- Automatically add it to a [[Price Book]]

## ❓ Rule to Remember
> Product = **what** we sell (no price, no customer, no deal info)
> Price lives in → [[Price Book Entry]]
> Sold in a deal via → [[Opportunity Product]]

Same Product across different countries/prices = **still one Product record**, never duplicated.
نفس المنتج بأسعار مختلفة = Product واحد فقط، لا ننشئ نسخًا متعددة

---
### 🔗 Related Notes
[[Account]] | [[Opportunity]] | [[Price Book]] | [[Price Book Entry]] | [[Opportunity Product]]
