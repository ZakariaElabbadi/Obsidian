---
tags: [salesforce, sales-cloud, object]
aliases: [OpportunityLineItem, Line Item]
---

# 🧩 Opportunity Product

## 📌 Definition
**Opportunity Product** (technical name: `OpportunityLineItem`) = the object that links a specific **Product** to a specific **Opportunity**, with quantity and pricing details.
(يربط بين المنتج وصفقة معينة، مع الكمية والسعر)

> You may see the name **OpportunityLineItem** in Flows or Apex — it's the same object.

## 🧠 Core Idea
An [[Opportunity]] can include **more than one product**:
- Generator 1500kW
- Battery
- Installation Service
- Warranty

A single field on Opportunity can't point to multiple products at once.
(Opportunity لا تستطيع أن تخزن أكثر من منتج بحقل واحد)

So Salesforce uses a separate object — **Opportunity Product** — where **each row = one product line** in the deal.
(كل سطر يمثل منتجًا واحدًا داخل الصفقة)

## 💡 Example
Opportunity: **CRM Project**
Customer wants: **Generator 1500kW**, Quantity: 2, Price: $25,000

| Opportunity | Product | Qty | Unit Price |
|---|---|---|---|
| CRM Project | Generator 1500kW | 2 | $25,000 |

Notice it stores more than just the product:
- Quantity (الكمية)
- Discount, if any (الخصم إن وجد)
- Total Price (السعر الإجمالي)

## 🔑 Why Link to Price Book Entry, Not Product Directly?
This is a classic Salesforce interview question. 😄
(هذا سؤال مقابلات العمل)

Because [[Product]] does **not** contain the price.
[[Price Book Entry]] contains all three needed pieces:
- The Product
- The Price Book
- The Price

So when creating an Opportunity Product, Salesforce requires a:
> **Price Book Entry ID** — not a Product ID.
(تحتاج إلى Price Book Entry ID، وليس Product ID)

## 🔗 Full Relationship Map
```
Opportunity
     │
     ▼
Opportunity Product   ← links Opportunity + Price Book Entry (+ Qty, Discount)
     │
     ▼
Price Book Entry       ← links Product + Price Book + Price
     ▲
     │
  ┌──┴──────────┐
  ▼             ▼
Product      Price Book
```

## ⚙️ Why This Flow Order Makes Sense
```
1. Get Price Book        → Which price list are we using?
2. Get Product            → Which product are we selling?
3. Get Price Book Entry    → What's the price of this product in this price book?
4. Create Opportunity Product → Add the product (with qty & price) to the deal
```

Each step depends on the one before it — you can't create an Opportunity Product without
first knowing the Price Book Entry, and you can't know that without first knowing which
Price Book and which Product you're working with.
(كل خطوة تعتمد على التي قبلها منطقيًا)

## 🗺️ The Complete Picture
```
Lead
 │
 ▼
Convert
 │
 ├──────────────┐
 ▼              ▼
Account      Contact
 │
 ▼
Opportunity
 │
 ▼
Opportunity Product
 │
 ▼
Price Book Entry
 ▲
 │
 ├──────────┐
 ▼          ▼
Product   Price Book
```

## ❓ Rule to Remember
> Opportunity Product = **one line item** inside a deal (product + qty + price)
> Always requires a → [[Price Book Entry]] (never a raw [[Product]] ID)
> One [[Opportunity]] → Many Opportunity Products (multiple items per deal)

---
### 🔗 Related Notes
[[Opportunity]] | [[Product]] | [[Price Book]] | [[Price Book Entry]]
