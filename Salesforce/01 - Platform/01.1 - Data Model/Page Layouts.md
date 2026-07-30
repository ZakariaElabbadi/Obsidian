---
tags: [salesforce, platform, concept]
aliases: [Page Layout]
---

# 🖼️ Page Layouts

## 📌 Definition
**Page Layout** = controls **which Fields, Related Lists, and Buttons appear** on a record's detail/edit page.
(يتحكم في أي الحقول والقوائم المرتبطة والأزرار تظهر على صفحة السجل)

> Page Layout is about **arrangement and visibility of the UI**, not about permissions.
(يتعلق بترتيب وإظهار الواجهة، وليس بالصلاحيات)

## 🧠 Core Idea
A Page Layout answers: **"When someone opens this record, what do they SEE on the page?"**
(عندما يفتح شخص هذا السجل، ماذا يرى على الصفحة؟)

## 🧾 What a Page Layout Controls
| Element | Example |
|---|---|
| Fields shown | Show "Discount %" on Opportunity Product, hide "Internal Notes" |
| Field order/sections | Group "Billing Info" fields together in one section |
| Required/Read-only (layout-level) | Make a field required just for this layout, without a full [[Validation Rules|Validation Rule]] |
| Related Lists | Show related [[Contact]]s and [[Opportunity]]s at the bottom of an [[Account]] page |
| Buttons & Actions | Show a custom "Send Quote" button on the Opportunity page |

## 💡 Real Example
```
Account Page Layout — "Customer" Record Type:
     Section: Company Info
        Account Name, Industry, Phone
     Section: Billing
        Billing Address, Payment Terms
     Related Lists:
        Contacts, Opportunities, Cases
     Buttons:
        New Opportunity, New Case
```
A Sales Rep opening a Customer Account sees exactly this layout — organized
and relevant to their work.
(الـ Sales Rep يرى بالضبط هذا الترتيب المنظم والمناسب لعمله)

## ⚖️ Page Layout vs Field-Level Security — Important Distinction
| | Page Layout | Field-Level Security (via [[Profiles]]/[[Permission Sets]]) |
|---|---|---|
| Controls | Whether a field appears **on this layout** | Whether the user can see/edit the field **at all**, anywhere |
| Overridable? | Layout can show a field... | ...but FLS can still hide it — FLS **always wins** |
| Analogy | "Where is it placed on the page?" | "Are you even allowed to know it exists?" |

⚠️ **Key exam point**: If a field is hidden by Field-Level Security, it will
**never** show on any Page Layout, even if the layout says to display it.
(إذا كان الحقل مخفيًا بواسطة FLS، فلن يظهر أبدًا حتى لو كان الـ Page Layout يعرضه)

## 🔗 Relation to Record Types
Different [[Record Types]] can each be assigned a **different Page Layout**.
(كل Record Type يمكن أن يُخصص له Page Layout مختلف)

```
Opportunity Object
     │
     ├── Record Type: New Business → Layout A (shows Lead Source)
     └── Record Type: Renewal      → Layout B (simplified, no Lead Source)
```

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Objects]] | A Page Layout is built for one specific Object |
| [[Fields]] | Determines which existing fields are visible/arranged, doesn't create new ones |
| [[Record Types]] | Different Record Types can use different Page Layouts |
| [[Profiles]] | Each Profile can be assigned a specific Page Layout per Record Type |

## ❓ Rule to Remember
> Page Layout = **what the page looks like** (شكل الصفحة وترتيبها)
> Controls fields, sections, related lists, and buttons — visual arrangement only.
> Field-Level Security always overrides Page Layout — if FLS hides a field, no layout can show it.

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Record Types]] | [[Profiles]] | [[Permission Sets]]
