---
tags: [salesforce, sales-cloud, object]
aliases: [Pricebook, Pricebook2]
---

# 📘 Price Book

## 📌 Definition
**Price Book** = a **price list**, not a product.
(قائمة أسعار، وليس منتجًا)

> A collection of prices for a group of products, grouped by context —
> such as region, customer type, or promotion.

## 🧠 Core Idea
Price Book answers the question:
**"Which price list are we using?"**

Multiple Price Books can hold the **same products**, but with **different prices**.
(كلها تحتوي على نفس المنتجات، لكن بأسعار مختلفة)

## 💡 Example
| Price Book | Purpose |
|---|---|
| Standard Price Book | Regular / default prices (الأسعار العادية) |
| VIP Price Book | Special discounted prices (أسعار خاصة) |
| Morocco Price Book | Prices for the Morocco market |
| USA Price Book | Prices for the USA market |

Same [[Product]] — **Dell Laptop** — across different Price Books:

| Price Book | Product | Price |
|---|---|---|
| Standard | Dell Laptop | $1,000 |
| VIP | Dell Laptop | $850 |
| Morocco | Dell Laptop | $900 |

Notice: the **Product never changed** — only the **price** attached to it changed depending on the Price Book.
(المنتج لم يتغير، الذي تغير هو السعر)

## ⚠️ Important Detail
Price Book does **not** store the Product and Price directly by itself.
(Price Book لا يخزن المنتج والسعر مباشرة)

So how does Salesforce know that "$900" belongs to "Dell Laptop" inside the "Morocco Price Book"?

👉 Through a separate linking object: **[[Price Book Entry]]**

```
Price Book
     │
     ▼
Price Book Entry   ← links Product + Price Book + Price together
     ▲
     │
     ▼
  Product
```

## 🔑 Special Note
Every Salesforce org has one default, permanent Price Book:
**Standard Price Book** — it cannot be deleted.
(موجود دائمًا بشكل افتراضي في كل Org، ولا يمكن حذفه)
Any additional Price Books (VIP, Regional, etc.) are called **Custom Price Books**.

## 🔗 Relationship to Other Objects
| Relationship | Description |
|---|---|
| Price Book → Price Book Entry | One Price Book can have many entries (one per product) |
| Price Book Entry → Product | Each entry links back to exactly one Product |

## ❓ Rule to Remember
> Price Book = the **list** (which price list are we using?)
> Price Book Entry = the **actual link** (product + price book + price)
> Product = the **item itself** (no price stored here)

Same product, multiple Price Books = multiple possible prices — but always **one Product record**.
(نفس المنتج، عدة قوائم أسعار = عدة أسعار محتملة، لكن دائمًا Product واحد فقط)

---
### 🔗 Related Notes
[[Product]] | [[Price Book Entry]] | [[Opportunity]] | [[Opportunity Product]]
