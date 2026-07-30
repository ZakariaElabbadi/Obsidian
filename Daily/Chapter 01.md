# Salesforce Admin Handbook
## Chapter 01 - Object Relationships & Flow Traversal

> Version: 1.0
> Language: English

---

# Learning Objectives

After completing this chapter, you should be able to:

- Understand Parent vs Child relationships.
- Identify Lookup and Master-Detail relationships.
- Decide when to use Direct Traversal.
- Decide when to use Get Records.
- Understand Collections and Loops.
- Build simple Record-Triggered Flows.

---

# Core Mental Model

Everything in Flow starts from **$Record**.

Ask yourself one question:

> "Do I need a Parent or do I need Children?"

---

# Parent vs Child

The object that **contains the Lookup field** is always the **Child**.

The object referenced by that Lookup is the **Parent**.

Example

Contact

- AccountId → Account
- OwnerId → User

Therefore

Child:
- Contact

Parents:
- Account
- User

---

# Relationship Rule

Child → Parent

- Direct Traversal
- No Get Records
- No Loop

Example

```
$Record.Account.Name
$Record.Owner.Email
$Record.Contact.Phone
```

---

Parent → Children

Requires

- Get Records
- Collection
- Loop

Example

Account

↓

Contacts

Flow

Get Records

Object = Contact

Filter

```
AccountId = $Record.AccountId
```

↓

Loop

---

# Golden Rule

```
Need Parent?
        │
        ▼
Direct Traversal

Need Children?
        │
        ▼
Get Records
        │
        ▼
Collection
        │
        ▼
Loop
```

---

# Object Relationship Map

```
                    User
                      ▲
                      │ OwnerId
                      │
                  Account
               /     |      \
              /      |       \
             ▼       ▼        ▼
        Contact  Opportunity  Case
              \      |
               \     ▼
                \ Opportunity Product
                 \
                  (via Account)
```

---

# Common Lookup Fields

## Account

Parents

- User (OwnerId)

Children

- Contact
- Opportunity
- Case

---

## Contact

Lookup Fields

- AccountId
- OwnerId

Parents

- Account
- User

---

## Opportunity

Lookup Fields

- AccountId
- OwnerId

Parents

- Account
- User

Children

- Opportunity Product

---

## Case

Lookup Fields

- AccountId
- ContactId
- OwnerId

Parents

- Account
- Contact
- User

---

# Flow Thinking Process

Before building any Flow:

## Step 1

What is the Trigger Object?

Example

Opportunity

↓

$Record is an Opportunity.

---

## Step 2

What data do I need?

Examples

Need Account?

↓

Direct

Need Owner?

↓

Direct

Need Contacts?

↓

Get Records

---

## Step 3

Is Get Records returning one record or many?

One record

↓

No Loop

Many records

↓

Loop

---

## Step 4

What should happen?

- Create Records
- Update Records
- Delete Records
- Send Email
- Call Action

---

# Example

Scenario

"When an Opportunity becomes Closed Won:

- Send an email to the Opportunity Owner.
- Create one Task for every Contact in the related Account."

Flow Design

```
Record Triggered Flow

↓

Opportunity

↓

After Save

↓

Stage = Closed Won

↓

Send Email

↓

Get Contacts

Filter

AccountId = $Record.AccountId

↓

Loop

↓

Create Task

WhoId = Current Contact.Id

WhatId = $Record.Id

OwnerId = $Record.OwnerId

↓

End
```

---

# Collections

A Collection is simply a list of records.

Example

```
Contact 1
Contact 2
Contact 3
Contact 4
```

Collections require a Loop to process each record.

---

# Loop

Loop processes one record at a time.

Example

```
Collection

↓

Contact 1

↓

Contact 2

↓

Contact 3

↓

Contact 4
```

---

# Common Mistakes

❌ Using Get Records to retrieve a Parent.

Correct

Use Direct Traversal.

---

❌ Forgetting to Loop through a Collection.

Correct

Collection

↓

Loop

---

❌ Filtering Contacts using OwnerId.

Correct

Filter using

```
AccountId = $Record.AccountId
```

---

❌ Confusing OwnerId with AccountId.

OwnerId

↓

User

AccountId

↓

Account

---

# Best Practices

✅ Use Entry Conditions whenever possible.

✅ Avoid unnecessary Decision elements.

✅ Use Direct Traversal whenever a Parent is available.

✅ Use Get Records only when retrieving Children.

✅ Think about the relationship before adding Flow elements.

---

# Interview Notes

Question

When do you use Get Records?

Answer

Whenever you need child records or records that are not already available through direct relationship traversal.

---

Question

When is a Loop required?

Answer

Whenever Get Records returns a Collection.

---

Question

Can I access a Parent without Get Records?

Answer

Yes.

Use Direct Traversal.

Example

```
$Record.Account.Name
```

---

# Superbadge Tips

Always ask yourself:

1. What is my Trigger Object?
2. What data do I need?
3. Parent or Children?
4. Do I need Get Records?
5. Is it a Collection?
6. Do I need a Loop?
7. What action should I perform?

---

# Key Takeaways

- Child contains the Lookup field.
- Parent is referenced by the Lookup field.
- Child → Parent = Direct Traversal.
- Parent → Children = Get Records.
- Collections require Loops.
- Always think before dragging Flow elements.
