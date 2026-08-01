---
tags:
  - Salesforce
  - Admin
  - Flow
  - DataModel
created:
---

# Salesforce Admin Map v1.0

> الهدف من هذا الملف هو فهم العلاقات بين Objects قبل بناء أي Flow.

---

# القاعدة الذهبية

قبل كتابة أي Flow اسأل نفسك:

1. أين أنا الآن؟ (Current Object)
2. هل أريد الوصول إلى Parent أم Children؟

إذا كانت الإجابة:

✅ Parent → استخدم Direct Relationship

إذا كانت:

✅ Children → استخدم Get Records ثم Loop

---

# مخطط العلاقات

```
                               Lead
                                 │
                            Convert
                                 │
                ┌────────────────┴────────────────┐
                ▼                                 ▼
            Account ◄──────────── Contact
               │                     ▲
               │                     │
               │                Parent = Account
               │
      ┌────────┼─────────────┐
      ▼        ▼             ▼
Opportunity   Case        Contact
      │
      ▼
Opportunity Product
      │
      ▼
Price Book Entry
   ▲            ▲
   │            │
Product     Price Book
```

---

# Objects

## Lead

Parent

- None

Children

- Converts to Account
- Converts to Contact

---

## Account

Parent

- None

Children

- Contact
- Opportunity
- Case

Direct Access

None

Get Records

- Contacts
- Opportunities
- Cases

---

## Contact

Parent

- Account

Children

- Cases (optional)

Direct Access

```text
$Record.Account.Name
$Record.Account.Industry
$Record.Account.Phone
```

Get Records

- Cases (later)

---

## Opportunity

Parent

- Account

Children

- Opportunity Products

Direct Access

```text
$Record.Account.Name
```

Get Records

- Opportunity Products

---

## Opportunity Product

Parent

- Opportunity
- Price Book Entry

Children

- None

Direct Access

```text
$Record.Opportunity.Name

$Record.PriceBookEntry.Product2.Name

$Record.PriceBookEntry.UnitPrice
```

---

## Price Book Entry

Parents

- Product
- Price Book

Children

- Opportunity Products

---

## Product

Children

- Price Book Entries

---

## Price Book

Children

- Price Book Entries

---

## Case

Parents

- Account
- Contact

Children

None

Direct Access

```text
$Record.Account.Name

$Record.Contact.Email
```

---

# قاعدة Flow

## إذا أردت Parent

```text
Child
   │
   ▲
Parent
```

Result

✅ Direct

Example

```text
$Record.Account.Name
```

---

## إذا أردت Children

```text
Parent
   │
   ▼
Children
```

Result

✅ Get Records

ثم

✅ Loop

---

# Reference Cards

## Assignment

Definition

> تغيير قيمة Variable أو Record موجود في الذاكرة.

Example

```text
$Record.StageName = "Qualification"
```

---

## Decision

Definition

> اتخاذ قرار اعتمادًا على شرط.

Example

```text
Amount > 10000 ?
```

---

## Get Records

Definition

> جلب Record أو Collection من قاعدة البيانات.

Example

```text
Get all Contacts
Where

AccountId = $Record.Id
```

---

# أهم قاعدة حتى الآن

```text
Parent
    ↑
 Direct

Children
    ↓
Get Records
    ↓
Loop
```

---

# سيتم إضافته في v2.0

- User
- Owner
- Queue
- Asset
- Contract
- Order
- Campaign
- Role
- Profile
- Permission Set
- Service Cloud Objects
- Relationship Traversal
- Record Triggered Flow Patterns
