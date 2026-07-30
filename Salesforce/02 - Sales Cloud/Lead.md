---
tags: [salesforce, sales-cloud, object]
aliases: [Potential Customer]
---

# 🎯 Lead

## 📌 Definition
**Lead** = a person or company who is **just interested**, not yet confirmed as a real customer.

> We haven't confirmed yet whether:
> - It's a real company ✅❌ (شركة حقيقية)
> - They have a budget ✅❌ (لديهم ميزانية)
> - They are serious about buying ✅❌ (جادون في الشراء)

## 🧠 Core Idea
A Lead is the **starting point** of the customer journey in Salesforce.
Everything begins here (نقطة البداية), and no other object is created before the Lead is verified.

## 🔄 What Happens to It?
A Lead either:
- ✅ Gets **Converted** → becomes [[Account]] + [[Contact]] (+ [[Opportunity]] if there's a real deal)
- ❌ Or gets rejected / closed (unqualified Lead)

```
Lead
 │
 │ (just an interested person / شخص مهتم فقط)
 ▼
Convert
 │
 ├── Account     (the Company / الشركة)
 ├── Contact     (the Person / الشخص)
 └── Opportunity (the Sales Deal / فرصة البيع)
```

## ⚠️ Important Rule
When converted, the three objects are created **only once** from the same Lead.
After conversion, we no longer use the Lead — all work moves fully to [[Account]], [[Contact]], and [[Opportunity]].
بعد التحويل، لا نعود نستخدم الـ Lead

## 🔗 Relationship to Other Objects
| Relationship | Description |
|---|---|
| Lead → Convert → Account | If confirmed as a real company (شركة حقيقية) |
| Lead → Convert → Contact | If the person is confirmed (تأكدنا من الشخص) |
| Lead → Convert → Opportunity | If there's an actual buying intent (نية شراء فعلية) |

## 💡 Real Example
> Ahmed fills a form on the company website and writes:
> "Interested in your products"
>
> At this moment, we only create a **Lead**.
> We don't yet know if his company is real, or if he will actually buy.

## ❓ Rule to Remember
> If the responsible person (e.g. Ali) leaves the company and Saad replaces him at the same company:
> - ✅ We do NOT create a new Account (لا ننشئ Account جديد)
> - ✅ We DO create a new Contact (ننشئ Contact جديد)
> - ✅ If there's a new deal, we create a new Opportunity (عند وجود صفقة جديدة)

---
### 🔗 Related Notes
[[Account]] | [[Contact]] | [[Opportunity]]
