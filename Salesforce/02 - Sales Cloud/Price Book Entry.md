---
tags: [salesforce, sales-cloud, object]
aliases: [PricebookEntry, PBE]
---

# 🔗 Price Book Entry

## 📌 Definition
**Price Book Entry** = the object that links a **Product**, a **Price Book**, and a **Price** together.
(يربط بين المنتج، قائمة الأسعار، والسعر)

> This is the real hero of Sales Cloud pricing. 😄
> (هذا هو البطل الحقيقي)

## 🧠 Core Idea
Neither [[Product]] nor [[Price Book]] stores the price alone.
- Product only knows: *"I am Dell Laptop"* (لا يعرف السعر ولا القائمة)
- Price Book only knows: *"I am a price list"* (لا يخزن المنتج والسعر مباشرة)

**Price Book Entry** is the missing piece that says:
> "This Product, in this Price Book, costs this much."

## 💡 Example
| Product | Price Book | Price |
|---|---|---|
| Dell Laptop | Standard | $1,000 |
| Dell Laptop | VIP | $850 |
| Dell Laptop | Morocco | $900 |

Each row here = **one Price Book Entry record**.
(كل سطر هو Record داخل Price Book Entry)

```
Price Book Entry
      │
      ├── Product      → Dell Laptop
      ├── Price Book    → Morocco Price Book
      └── Price         → $900
```

## 🧾 Key Fields
| Field | Meaning |
|---|---|
| Product | Which product this entry is for (المنتج) |
| Price Book | Which price list this entry belongs to (قائمة الأسعار) |
| List Price | The actual price (السعر) |
| Active | Is this price currently usable? (هل السعر مفعّل؟) |

## ⚠️ Why Design It This Way?
Because a single Product can have **many different prices** depending on the Price Book.
(لأن المنتج الواحد يمكن أن يكون له عدة أسعار)

If price lived directly on Product:
```
Product → Price
```
There would only be **one price ever** — not flexible enough for regions, VIP tiers, or promotions.

Instead, Salesforce separates it:
```
Product ──┐
           ├──► Price Book Entry ──► Price
Price Book ┘
```

## 🔗 Relationship to Other Objects
| Relationship | Description |
|---|---|
| Product → Price Book Entry | One Product can appear in many Price Book Entries (one per Price Book) |
| Price Book → Price Book Entry | One Price Book contains many entries (one per Product) |
| Price Book Entry → Opportunity Product | The entry is required to add a product to a deal |

## ⚙️ Why It Matters in Flows
This is the exact logic behind a common Flow pattern:

```
Get Price Book        → Which price list are we using?
     ↓
Get Product            → Which product are we selling?
     ↓
Get Price Book Entry    → What is the price of THIS product in THIS price book?
     ↓
Create Opportunity Product → Add it to the deal
```

Example: searching for `Generator 1500kW` in the `Standard` Price Book:

```
Price Book Entry found:
Product = Generator 1500kW
Price Book = Standard
Price = $25,000
```

Without Price Book Entry, the Flow would have **no way to know the price**.
(بدون Price Book Entry، لن يعرف الـ Flow السعر إطلاقًا)

## ❓ Rule to Remember
> Product = "what" (لا يعرف السعر)
> Price Book = "which list" (لا يخزن المنتج والسعر)
> Price Book Entry = "what + which list + how much" — all three together
> Always required before adding a product to an [[Opportunity]] via [[Opportunity Product]]

---
### 🔗 Related Notes
[[Product]] | [[Price Book]] | [[Opportunity]] | [[Opportunity Product]]
