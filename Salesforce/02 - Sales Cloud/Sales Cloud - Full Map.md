---
tags: [salesforce, sales-cloud, map]
aliases: [Full Diagram, Objects Map, Sales Cloud Map]
---

# 🗺️ Sales Cloud — Full Objects Map

## 📌 The Complete Diagram
(الخريطة الكاملة لكل الـ Objects التي درسناها)

```
                    Lead
                     │
               Convert Lead
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
      Account               Contact
          │
          ▼
     Opportunity
          │
          ▼
 Opportunity Product
          │
          ▼
   Price Book Entry
        ▲       ▲
        │       │
    Product   Price Book
```

## 🧭 How to Read This Map

| Step | Object | Question It Answers |
|---|---|---|
| 1 | [[Lead]] | Is this person/company even real? (شخص مهتم فقط) |
| 2 | [[Account]] | Who is the company? (الشركة) |
| 3 | [[Contact]] | Who is the person inside the company? (الشخص) |
| 4 | [[Opportunity]] | What deal are we working on? (الصفقة) |
| 5 | [[Opportunity Product]] | Which products are part of this deal? (منتجات الصفقة) |
| 6 | [[Price Book Entry]] | What's the price of this product, in this list? (الرابط بين المنتج والسعر) |
| 7 | [[Product]] | What are we actually selling? (المنتج نفسه) |
| 8 | [[Price Book]] | Which price list are we using? (قائمة الأسعار) |

## 🔑 Key Rule Behind the Whole Map
Every arrow in this diagram exists because **one single field cannot hold two answers at once**.
كل سهم في هذا المخطط موجود لأن حقلًا واحدًا لا يمكنه الإجابة عن سؤالين في نفس الوقت

- A Lead can become **two different things** → split into Account + Contact
- An Account can have **many deals** → separate Opportunity records
- An Opportunity can have **many products** → separate Opportunity Product records
- A Product can have **many prices** → separate Price Book Entry records (one per Price Book)

## ⚙️ Why This Exact Flow Order Makes Sense
```
1. Get Price Book         → Which price list?
2. Get Product             → Which product?
3. Get Price Book Entry     → Price of that product in that list
4. Create Opportunity Product → Add it to the deal
```

You cannot skip a step upward — each one depends on the result of the step before it.
لا يمكن تخطي أي خطوة، لأن كل خطوة تعتمد على التي قبلها

## 💡 Real Example — Full Journey
```
Ahmed fills a form           → Lead
        │ Convert
        ▼
Microsoft (Account) + Ahmed (Contact)
        │
        ▼
"CRM Project" (Opportunity)
        │
        ▼
Adds "Generator 1500kW" x2   → Opportunity Product
        │
        ▼
Looks up price in "Standard" → Price Book Entry ($25,000)
        ▲            ▲
        │            │
   Generator 1500kW   Standard Price Book
    (Product)          (Price Book)
```

## ❓ One-Line Summary for Each Object
> - **Lead** → not yet confirmed (غير مؤكد)
> - **Account** → the company (الشركة)
> - **Contact** → the person (الشخص)
> - **Opportunity** → the deal (الصفقة)
> - **Product** → the item sold (المنتج)
> - **Price Book** → the price list (قائمة الأسعار)
> - **Price Book Entry** → product + price book + price (الربط بين الثلاثة)
> - **Opportunity Product** → one line item inside a deal (سطر منتج داخل الصفقة)

---
### 🔗 Related Notes
[[Lead]] | [[Account]] | [[Contact]] | [[Opportunity]] | [[Product]] | [[Price Book]] | [[Price Book Entry]] | [[Opportunity Product]]
