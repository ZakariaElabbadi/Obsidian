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

```
Subject: Congratulations!
Body:
Hello John,
Your Opportunity has been Closed Won.
Thank you.
```

## 2. Use Email Template
Instead of writing the email, Salesforce uses an existing Email Template.

```
Opportunity Closed Won
```

**Advantages:** Easy maintenance, reusable, consistent branding, professional.

---

# Configure Recipient Details

> **Who will receive the email?**

## Recipient Type
Before filling in Recipient Address/ID, you choose **what kind of recipient** you're sending to. This determines how the rest of the recipient fields behave:

| Recipient Type | What you provide |
|---|---|
| **Email Address** | A raw email string (e.g. `customer@gmail.com`) or merge field |
| **User** | A User record Id |
| **Contact** | A Contact record Id |
| **Lead** | A Lead record Id |
| **Person Account** | A Person Account record Id |

> This field is what tells the action *how to interpret* the Recipient ID you provide below — get it wrong and the email fails to resolve an address.

## Recipient Addresses
Send the email directly to one or more email addresses.

```
customer@gmail.com
{!Contact.Email}
{!Lead.Email}
```

**Use when:** You already know the email address.

## CC Addresses (Carbon Copy)
Everyone can see who received the CC.
```
To:  client@gmail.com
CC:  manager@company.com
```

## BCC Addresses (Blind Carbon Copy)
Recipients cannot see the BCC addresses.
```
To:   client@gmail.com
BCC:  director@company.com
```

## Recipient ID
Instead of an email address, provide a Salesforce **Record ID**. Supported: Contact, Lead, User.
```
{!Contact.Id}
```
Salesforce automatically finds the email tied to that record.

**Advantages:** Safer, dynamic, no hardcoded email.

## 📦 Sending to Multiple Recipients (Bulk)
Just like Create/Update Records, the Send Email action can accept a **Collection** of recipient addresses/IDs rather than a single value — letting you email an entire list in **one action call** instead of looping and calling Send Email once per recipient.

> Follow the same bulkification pattern used elsewhere in Flow: **build the recipient collection first (Loop + Assignment), then call Send Email once after the loop** — not inside it. See the Loop and Assignment references for this pattern.

---

# Configure Sender Details

> **Who is sending the email?**

## Sender Type

### Current User
Email is sent from the current logged-in user.

### Organization-Wide Email Address
```
support@company.com
```
**Best for:** Customer Support, Sales Team, Marketing.

### Default Workflow User
Email comes from the Workflow User.

### Automated Process
Email is sent by the Automated Process User.

## Sender Email Address
When using Organization-Wide Email, choose one of the **verified** email addresses.
```
support@company.com
sales@company.com
info@company.com
```

> ⚠️ The address must already be a **verified** Organization-Wide Email Address in Setup — an unverified address will fail at runtime.

---

# Configure Email Content

## Subject
```
Opportunity Closed Successfully
```
**Dynamic Example:**
```
"Opportunity: " & {!$Record.Name}
```
Result: `Opportunity: ABC Corporation`

## Body
**Simple:**
```
Hello,
Your Opportunity has been Closed Won.
Thank you.
```
**Dynamic:**
```
Hello {!$Record.Owner.FirstName},
Congratulations!
Opportunity: {!$Record.Name}
Amount: {!$Record.Amount}
```

## Rich Text
Supported: Bold, Italic, Underline, Colors, Lists, Images, Links, Alignment. Perfect for professional emails.

## Images
Inserted directly inside the email body. Useful for company logos, product images, banners.

## Hyperlinks
```
https://company.com
```
Can also be displayed as: `Click Here`

## Text Alignment
Left, Center, Right

## Lists
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
Instead of composing the email manually, select an Email Template.

**Benefits:** Easy maintenance, reusable, professional branding, shared by multiple Flows.

---

# Use Line Breaks
When using Formula Resources, this option correctly interprets line breaks. Usually **Enabled**.

---

# Attachment ID
Attach one file. Usually a `ContentDocument` or `Attachment` Record ID.

# Attachment ID Collection
Attach multiple files.
```
Invoice.pdf
Contract.pdf
Image.png
```

---

# Related Record ID
Links the email to a Salesforce record.
```
Opportunity Id
Case Id
Account Id
```
**Benefit:** The email appears inside the **Activity Timeline** / **Activity History** of that record.

---

# Recipient Address vs Recipient ID

| | Value | Behavior |
|---|---|---|
| **Recipient Address** | `customer@gmail.com` | Sent as-is, no Salesforce lookup |
| **Recipient ID** | `003XXXXXXXXXXXX` | Salesforce automatically finds the linked email |

---

# ⚠️ Two Gotchas That Break Emails in Production

## 1. Org Email Deliverability Setting
Even a perfectly configured Send Email action **won't send anything** if your org's **Email Deliverability Access Level** (Setup → Email Administration → Deliverability) is set to **"No Access"** or **"System Email Only."** Set it to **"All Email"** for Flow-sent emails to actually go out — a very common cause of "the Flow ran fine but no email arrived."

## 2. Real Emails Send During Testing
Unlike Get/Create/Update Records (which you can safely test with sandbox or debug data), running **Send Email** during Flow debugging/testing sends a **real email** to whatever address is configured. Always test with your own address or a sandbox email address, never with real customer data, to avoid spamming actual contacts.

---

# 🚦 Governor Limits & Loop Placement

Like DML and SOQL, sending email has **per-transaction limits** (check current Salesforce limits, as they can change by release/edition). The same rule from Loop/Create Records applies:

> **Never call Send Email inside a Loop** for a per-record email. Build a recipient collection and call Send Email **once** with the whole collection, or route through a proper bulk-email tool if volume is high.

---

# ✅ Best Practices

- Never hardcode email addresses.
- Prefer **Recipient ID** over Recipient Address when possible (safer, dynamic).
- Use **Email Templates** for production-grade, maintainable emails.
- Use **Organization-Wide Email Address** for support/sales/marketing sends.
- Always set **Related Record ID** so the email shows in the record's Activity Timeline.
- Use **Rich Text** for professional formatting.
- Confirm the org's **Email Deliverability** setting is "All Email" before going live.
- Batch recipients into a **Collection** and send once, rather than looping.
- Test with your own address first — Send Email fires for real during debugging.

# ❌ Common Mistakes

- Setting **Recipient Type** to one kind (e.g. Contact) but mapping in an ID from a different object (e.g. Lead) — the lookup fails.
- Using an unverified Organization-Wide Email Address as the sender.
- Forgetting **Related Record ID** — the email sends but is invisible on the record's timeline.
- Calling Send Email inside a Loop instead of batching recipients.
- Testing with real customer email addresses.
- Assuming the email sent successfully just because the Flow didn't error — deliverability settings can silently block sending.

---

# Real-World Examples

**Example 1**
```
Opportunity Closed Won → Send Congratulations Email → Opportunity Owner
```

**Example 2**
```
Case Priority = High → Notify Support Manager
```

**Example 3**
```
New Customer Created → Send Welcome Email
```

**Example 4**
```
Invoice Generated → Attach PDF → Email Customer
```

**Example 5**
```
Contract Approved → Notify Sales Rep → Notify Customer → Attach Contract PDF
```

---

# Summary

| Feature | Purpose |
|----------|---------|
| Recipient Type | Determines how Recipient Address/ID is interpreted |
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
| Related Record ID | Link email to Salesforce record (Activity Timeline) |
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