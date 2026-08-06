---
tags: [salesforce, sales-ops, sales-process, crm]
title: An Organized Approach to Selling — Sales Process & Sales Team Roles
---

# An Organized Approach to Selling

## 🎯 Big Picture

Sales is a complex process — repeated touch points, time, effort, and (especially in B2B) buy-in from multiple stakeholders — just to close **one** deal. That's why most companies define a **sales process**: a repeatable set of steps to move a prospect from first awareness to a closed sale.

> As a Sales Ops Specialist, your job is to help **optimize** this process. CRMs like Salesforce Sales Cloud are literally built around it.

---

## 🔗 The 5 Stages of a Typical B2B Sales Process

```
Prospecting → Qualifying → Presenting → Closing → Customer Success
```

| Stage | What Happens | Primary CRM Tool |
|---|---|---|
| **1. Prospecting** | Identify potential customers (leads) | Sales Cloud — Lead Management |
| **2. Qualifying** | Vet leads for need + ability to pay | Sales Cloud — Lead & Opportunity Management |
| **3. Presenting** | Pitch the product/service, handle objections | Sales Cloud — Opportunity Management |
| **4. Closing** | Finalize terms, get the signature | Sales Cloud — Opportunity Management |
| **5. Customer Success** | Post-sale support, retention, referrals | Service Cloud — Customer Success Management |

---

## Stage 1 — Prospecting

**Prospecting** (a.k.a. **lead generation**) = identifying potential customers.

A **lead** = an individual/organization with expressed interest in what you're selling.

| Lead Type | Definition | Example |
|---|---|---|
| **Inbound** | Comes *to* the business on its own (visits site, downloads eBook, subscribes to blog) | A signup on the company's email list |
| **Outbound** | The business *seeks out* the lead (cold calling, purchased lead lists) | A cold call from an SDR |

> 📖 Example: **Maha** (Marketing Associate) spots **Casper** on Yum2Go's email signup list → Casper becomes an **inbound lead**.

---

## Stage 2 — Qualifying

**Qualifying** = evaluating whether a lead (a) has a real need for the product/service and (b) can afford it. Think of it as a **filter** between "lead" and "prospect."

Qualifying happens in **two rounds**:

1. **Marketing round** → produces a **Marketing Qualified Lead (MQL)**
2. **Sales round** (by an SDR) → produces a **Sales Qualified Lead (SQL)**, now called a **prospect**

| Term | Who decides | Meaning |
|---|---|---|
| **MQL** (Marketing Qualified Lead) | Marketing team | Ready to hand off to sales for a follow-up |
| **SQL** (Sales Qualified Lead) | SDR (Sales Development Rep) | Vetted and worth pursuing as a prospect |
| **Prospect** | — | A lead qualified as fitting certain criteria |

### 🧭 Frameworks used to qualify (referenced, defined here for clarity)
- **ICP (Ideal Customer Profile)** — a description of the "perfect fit" customer a company should be targeting, based on firmographics, needs, and buying behavior.
- **BANT** — a classic qualification framework checking four things about a lead:
  - **B**udget — can they afford it?
  - **A**uthority — are they the decision-maker (or can they influence one)?
  - **N**eed — do they have a real problem this solves?
  - **T**imeline — when do they need a solution?

> 📖 Example: **Salvador** (SDR) emails **Casper** to ask what he needs from a food distributor. Casper explains he needs deliveries 3x/week to 5 Bay Area locations.

---

## Stage 3 — Presenting

Once a lead is an SQL/prospect and a meeting is set, the deal officially starts moving toward close. The prospect is typically **handed off from the SDR to an Account Executive (AE)**.

The AE:
- Presents the product/service as a solution to the prospect's specific problem
- Schedules demos/presentations (often across multiple meetings)
- Researches stakeholders to prepare
- Develops tailored recommendations
- **Handles objections** (price, timing, fear of change) by demonstrating value and the cost of *not* buying

> 📖 Example: **Salvador** sets up a meeting between **Amber** (AE) and **Casper**. Casper needs to loop in his team, so a follow-up call is scheduled.

---

## Stage 4 — Closing

Everything needed to get a signed contract and turn a prospect into a **customer**.

The AE:
- Delivers a formal proposal based on agreed terms
- Negotiates final pricing
- Clears remaining roadblocks until the prospect signs

> 📖 Example: **Amber** follows up after the last call — **Casper decides to move forward** with Yum2Go.

---

## Stage 5 — Customer Success

The relationship **doesn't end at signature** — the ongoing business relationship is what lasts (and drives repeat business + referrals).

The AE hands the new customer to a **Customer Success Manager (CSM)**, who:
- Supports onboarding
- Checks in on evolving needs, configures the product/service accordingly
- Proactively nurtures the relationship

> 📖 Example: **Ciara** (CSM) emails Casper to help set up the delivery schedule and offers ongoing support.

---

## 👥 Sales Team Roles ("Sales Force")

The **sales force** = everyone responsible for selling a company's products/services. Roles may span both marketing and sales departments (more common in larger companies).

| Role | Character | Primary Stage(s) | Core Responsibility |
|---|---|---|---|
| **Marketing Associate** | Maha | Prospecting | Generates MQLs |
| **Sales Development Rep (SDR)** | Salvador | Qualifying (+ some Prospecting for outbound) | Vets MQLs into SQLs/prospects, sets up first meeting |
| **Account Executive (AE)** | Amber | Presenting, Closing | Presents, demos, handles objections, closes the deal |
| **Customer Success Manager (CSM)** | Ciara | Customer Success | Onboards, supports, retains the customer |
| **Sales Manager** | Sammy | *All stages* (oversight) | Guides the team, evaluates performance, forecasts sales, tracks metrics |

> All of these people are **CRM business users (end users)** — the employees who use Salesforce day-to-day. Understanding their workflows is what lets a Sales Ops Specialist configure Salesforce to actually help them.

---

## 🧩 Full Handoff Chain

```
Marketing Associate (Maha)
      ↓ MQL
Sales Development Rep (Salvador)
      ↓ SQL / Prospect
Account Executive (Amber)
      ↓ Closed-Won Customer
Customer Success Manager (Ciara)
```
*(Sales Manager — Sammy — oversees the whole chain throughout.)*

---

## 📖 Key Terms Glossary

| Term | Definition |
|---|---|
| **Sales** | All activities involved in selling a product/service to a consumer or business |
| **B2C** | Selling directly to consumers |
| **B2B** | Selling to other businesses |
| **Sales process** | Repeatable steps to move a prospect from awareness to closed sale |
| **Lead** | An individual/org with expressed interest |
| **Prospecting** | Identifying potential customers (a.k.a. lead generation) |
| **Inbound lead** | Comes to the business on its own |
| **Outbound lead** | Business seeks the lead out |
| **Qualifying** | Evaluating need + ability to pay |
| **Prospect** | A lead qualified as fitting certain criteria |
| **MQL** | Marketing-qualified, ready for sales follow-up |
| **SQL** | Sales-vetted, worth pursuing |
| **Sales force** | Everyone responsible for selling the company's offerings |
| **CRM business user / end user** | Employee who uses the CRM in daily workflow |

---

## ✅ Key Takeaways

1. **Sales** covers everything involved in selling — **B2C** sells to consumers directly, **B2B** sells to other businesses and tends to have longer, more stakeholder-heavy cycles.
2. A **sales process** is a repeatable, multi-stage framework (Prospecting → Qualifying → Presenting → Closing → Customer Success) that CRMs are structured around.
3. Different **roles** own different stages — Marketing Associate, SDR, AE, CSM, and Sales Manager (oversight) — and each interacts with the CRM differently based on their stage.
4. Every company customizes this process differently based on size, industry, and business model — but the underlying Salesforce skills transfer regardless of the specific variation.
