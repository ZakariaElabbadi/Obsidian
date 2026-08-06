---
tags:
  - Salesforce
  - Flow
  - Email
  - Automation
  - CRM
created: 2026-08-06
---

# 📧 Salesforce Flow - Send Email Action

> **Goal:** Learn every field available in the **Send Email** action and understand when and why to use it.

---

# Overview

The **Send Email** Action allows a Flow to automatically send emails to users, contacts, leads, or external email addresses.

Common use cases:

- Welcome emails
- Opportunity notifications
- Case updates
- Approval notifications
- Reminder emails
- Marketing follow-ups

---

# Two Ways to Send an Email

## 1. Compose Email Content

You create everything inside the Flow.

- Subject
- Body
- Images
- Links
- Formatting

Example

```
Subject:
Congratulations!

Body:
Hello John,

Your Opportunity has been Closed Won.

Thank you.
```

---

## 2. Use Email Template

Instead of writing the email, Salesforce uses an existing Email Template.

Example

```
Opportunity Closed Won
```

Advantages

- Easy maintenance
- Reusable
- Consistent branding
- Professional

---

# Configure Recipient Details

This section answers one question:

> **Who will receive the email?**

---

## Recipient Addresses

Send the email directly to one or more email addresses.

Examples

```
customer@gmail.com
```

or

```
{!Contact.Email}
```

or

```
{!Lead.Email}
```

Use when:

- You already know the email address.

---

## CC Addresses

Carbon Copy

Everyone can see who received the CC.

Example

To

```
client@gmail.com
```

CC

```
manager@company.com
```

---

## BCC Addresses

Blind Carbon Copy

Recipients cannot see the BCC addresses.

Example

To

```
client@gmail.com
```

BCC

```
director@company.com
```

---

## Recipient ID

Instead of an email address, provide a Salesforce Record ID.

Supported records include:

- Contact
- Lead
- User

Example

```
{!Contact.Id}
```

Salesforce automatically finds the email.

Advantages

- Safer
- Dynamic
- No hardcoded email

---

# Configure Sender Details

This section defines:

> **Who is sending the email?**

---

## Sender Type

Common options

### Current User

Email is sent from the current logged-in user.

---

### Organization-Wide Email Address

Example

```
support@company.com
```

Best for

- Customer Support
- Sales Team
- Marketing

---

### Default Workflow User

Email comes from the Workflow User.

---

### Automated Process

Email is sent by the Automated Process User.

---

## Sender Email Address

When using Organization-Wide Email,

choose one of the verified email addresses.

Example

```
support@company.com
sales@company.com
info@company.com
```

---

# Configure Email Content

This section defines:

- Subject
- Body
- Formatting

---

# Subject

Example

```
Opportunity Closed Successfully
```

Dynamic Example

```
"Opportunity: " &
{!$Record.Name}
```

Result

```
Opportunity: ABC Corporation
```

---

# Body

Simple Example

```
Hello,

Your Opportunity has been Closed Won.

Thank you.
```

Dynamic Example

```
Hello {!$Record.Owner.FirstName},

Congratulations!

Opportunity:
{!$Record.Name}

Amount:
{!$Record.Amount}
```

---

# Rich Text

Rich Text allows formatting.

Supported features

- Bold
- Italic
- Underline
- Colors
- Lists
- Images
- Links
- Alignment

Perfect for professional emails.

---

# Images

Images can be inserted directly inside the email body.

Useful for

- Company Logo
- Product Images
- Banners

---

# Hyperlinks

Example

```
https://company.com
```

Can also be displayed as

```
Click Here
```

---

# Text Alignment

Options

- Left
- Center
- Right

---

# Lists

Example

```
• Task One

• Task Two

• Task Three
```

or

```
1. First

2. Second

3. Third
```

---

# Use Email Template

Instead of composing the email manually,

select an Email Template.

Benefits

- Easy maintenance
- Reusable
- Professional branding
- Shared by multiple Flows

---

# Use Line Breaks

When using Formula Resources,

this option correctly interprets line breaks.

Usually

```
Enabled
```

---

# Attachment ID

Attach one file.

Usually a

```
ContentDocument
```

or

```
Attachment
```

Record ID.

---

# Attachment ID Collection

Attach multiple files.

Example

- Invoice.pdf

- Contract.pdf

- Image.png

---

# Related Record ID

Links the email to a Salesforce record.

Examples

```
Opportunity Id
```

```
Case Id
```

```
Account Id
```

Benefits

The email appears inside

```
Activity Timeline
```

or

```
Activity History
```

---

# Recipient Address vs Recipient ID

Recipient Address

```
customer@gmail.com
```

Recipient ID

```
003XXXXXXXXXXXX
```

Salesforce automatically finds the email.

---

# Best Practices

✅ Never hardcode email addresses.

✅ Prefer Recipient ID when possible.

✅ Use Email Templates for production.

✅ Use Organization-Wide Email Address.

✅ Always relate the email to the record.

✅ Use Rich Text for professional formatting.

---

# Real-World Examples

## Example 1

Opportunity Closed Won

↓

Send Congratulations Email

↓

Opportunity Owner

---

## Example 2

Case Priority = High

↓

Notify Support Manager

---

## Example 3

New Customer Created

↓

Send Welcome Email

---

## Example 4

Invoice Generated

↓

Attach PDF

↓

Email Customer

---

## Example 5

Contract Approved

↓

Notify Sales Rep

↓

Notify Customer

↓

Attach Contract PDF

---

# Summary

| Feature | Purpose |
|----------|---------|
| Recipient Address | Send to an email address |
| Recipient ID | Send using Contact/Lead/User ID |
| CC | Visible copy |
| BCC | Hidden copy |
| Subject | Email title |
| Body | Email content |
| Rich Text | Professional formatting |
| Email Template | Reusable email |
| Attachment ID | One attachment |
| Attachment Collection | Multiple attachments |
| Related Record ID | Link email to Salesforce record |
| Sender Type | Choose who sends the email |

---

# What We Will Learn Next

- HTML Emails
- CSS Styling
- Dynamic Images
- PDF Attachments
- Email Templates
- ContentVersion & ContentDocument
- Professional Notification System
- Complete Email Automation Project