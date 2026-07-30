---
tags: [salesforce, admin, flow, object-relationships, day08]
title: Salesforce Admin - Day 08 - Object Relationships & Flow Traversal
---

# Salesforce Admin - Day 08
## Topic: Object Relationships & Flow Traversal

---

# 🧠 Mental Model

## Golden Rule
> The object that **contains** the Lookup field is the **Child**.
> The object **referenced** by the Lookup field is the **Parent**.

**Example:**
```
Contact
   |
   | AccountId (Lookup)
   ▼
Account
```
- Child = **Contact**
- Parent = **Account**

---

# ⬇️ Parent → Child

Requires:
- Get Records
- Collection
- Loop

**Example:**
```
Account
   ↓
Contacts
```

Flow:
```
Get Contacts
Filter: AccountId = $Record.Id
```

---

# ⬆️ Child → Parent

Direct traversal. **No Get Records required.**

Examples:
- `$Record.Account.Name`
- `$Record.Owner.Email`
- `$Record.Contact.Phone`

---

# 🔗 Lookup Fields Reference

## Opportunity
| Field | Parent |
|---|---|
| AccountId | Account |
| OwnerId | User |

## Contact
| Field | Parent |
|---|---|
| AccountId | Account |
| OwnerId | User |

## Case
| Field | Parent |
|---|---|
| AccountId | Account |
| ContactId | Contact |
| OwnerId | User |

---

# 📏 Flow Golden Rules

1. **Child → Parent** – direct access
   `$Record.Account.Name`
2. **Parent → Child** – requires Get Records + Loop
3. **Collection** – loop over every record
4. **Updating records** – Loop → Assignment → Update Records (once, after loop)
5. **Creating records** – Loop → Create Records

---

# ✅ Best Practices

- Update collections **once**, after the Loop — not inside it.
- Use direct traversal whenever possible.
- Avoid unnecessary Get Records elements.

---

# ❌ Common Mistakes

- Thinking **Contact** is the parent of **Opportunity**.

**Correct structure:**
```
Account
├── Contact
└── Opportunity
```
There is **no direct relationship** between Contact and Opportunity.

---

# ❓ Quick Quiz

**Q1:** Which object is the Parent?
```
Opportunity
   |
AccountId
```
**A:** Account

---

**Q2:** How do you access an Opportunity's Account Name?
**A:** `$Record.Account.Name`

---

**Q3:** How do you retrieve all Contacts of an Account?
**A:**
```
Get Records
Filter: AccountId = $Record.Id
Loop
```
