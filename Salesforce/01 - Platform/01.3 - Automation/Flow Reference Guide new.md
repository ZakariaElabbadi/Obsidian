---
tags: [salesforce, map, schema, flow, reference]
aliases: [Flow Reference Guide, Zakaria's Guide, Direct vs Get Records Map]
---

# 🧭 Flow Reference Guide — Direct vs Get Records

> 🔁 **Living document** — grows every time we learn a new Object.
> Look here BEFORE building any Flow. Ask yourself: am I going ⬆️ UP or ⬇️ DOWN?

## 🗺️ The Master Diagram

```
                                Lead
                                  │
                              Convert
                                  │
                    ┌─────────────┴─────────────┐
                    ▼                           ▼
                Account ◄──────────────────── Contact
                    ▲                        (Child)
                    │ ⬆ Direct
                    │
        ┌───────────┼───────────────┐
        ▼ ⬇ Get Records              ▼ ⬇ Get Records
    Contact                       Opportunity ──────── Case
                                       │
                                       │ (Master-Detail)
                                       ▼ ⬇ Get Records
                              Opportunity Product
                                       │
                                       │ ⬆ Direct (Lookup)
                                       ▼
                              Price Book Entry
                                  ▲         ▲
                             ⬆ Direct   ⬆ Direct
                                  │         │
                              Product   Price Book
```

### Legend
```
⬆ Direct       = Child → Parent   → {!Record.ParentField.Name}   (ONE record, no loop)
⬇ Get Records  = Parent → Child   → new Get Records + Loop        (MANY records, collection)
```

## 📖 Per-Object Breakdown ("دليل زكريا")

### Lead
```
Lead
│
├── Parent
│     └── (none — Lead is a starting point)
│
├── Children
│     └── (none — Lead converts INTO Account/Contact/Opportunity)
│
├── Up (Child → Parent)
│     ❌ Not applicable
│
└── Down (Parent → Child)
      ❌ Not applicable — use "Convert Lead" action instead
```

### Account
```
Account
│
├── Parent
│     └── (none — Account is usually top-level)
│
├── Children
│     ├── Contacts
│     ├── Opportunities
│     └── Cases
│
├── Up (Child → Parent)
│     ❌ Not applicable (no parent above it)
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: AccountId = {!Record.Id})
```

### Contact
```
Contact
│
├── Parent
│     └── Account
│
├── Children
│     └── Cases (sometimes, via ContactId on Case)
│
├── Up (Child → Parent)
│     ✅ Direct → {!Record.Account.Name}
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: ContactId = {!Record.Id})
```

### Opportunity
```
Opportunity
│
├── Parent
│     └── Account
│
├── Children
│     └── Opportunity Products (Master-Detail)
│
├── Up (Child → Parent)
│     ✅ Direct → {!Record.Account.Name}
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: OpportunityId = {!Record.Id})
```

### Case
```
Case
│
├── Parent
│     ├── Account
│     └── Contact
│
├── Children
│     └── (none covered yet)
│
├── Up (Child → Parent)
│     ✅ Direct → {!Record.Account.Name}
│     ✅ Direct → {!Record.Contact.Name}
│
└── Down (Parent → Child)
      ❌ Not applicable yet
```

### Opportunity Product
```
Opportunity Product (OpportunityLineItem)
│
├── Parent
│     ├── Opportunity (Master-Detail)
│     └── Price Book Entry (Lookup)
│
├── Children
│     └── (none)
│
├── Up (Child → Parent)
│     ✅ Direct → {!Record.OpportunityId.Name}
│     ✅ Direct → {!Record.PriceBookEntryId.UnitPrice}
│     ✅ Direct → {!Record.PriceBookEntryId.Product2.Name}
│
└── Down (Parent → Child)
      ❌ Not applicable
```

### Product
```
Product (Product2)
│
├── Parent
│     └── (none)
│
├── Children
│     └── Price Book Entries
│
├── Up (Child → Parent)
│     ❌ Not applicable
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: Product2Id = {!Record.Id})
```

### Price Book
```
Price Book (Pricebook2)
│
├── Parent
│     └── (none)
│
├── Children
│     └── Price Book Entries
│
├── Up (Child → Parent)
│     ❌ Not applicable
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: Pricebook2Id = {!Record.Id})
```

### Price Book Entry
```
Price Book Entry (PricebookEntry)
│
├── Parent
│     ├── Product (Product2)
│     └── Price Book (Pricebook2)
│
├── Children
│     └── Opportunity Products
│
├── Up (Child → Parent)
│     ✅ Direct → {!Record.Product2.Name}
│     ✅ Direct → {!Record.Pricebook2.Name}
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: PricebookEntryId = {!Record.Id})
```

### User / Owner
```
User
│
├── Parent
│     └── Manager (self-relationship, User → User)
│
├── Children
│     └── Direct Reports (other Users where ManagerId = this User)
│
├── Up (Child → Parent)
│     ✅ Direct → {!Record.Manager.Name}
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: ManagerId = {!Record.Id})
```
⚠️ **"Owner" is not a separate Object** — it's a special field (`OwnerId`)
that exists on almost every Object (Account, Contact, Opportunity, Lead,
Case...). It's **polymorphic**: it can point to either a **User** or a
**Queue**.
```
Any Record
│
├── Up (Child → Parent, via OwnerId)
│     ✅ Direct → {!Record.Owner.Name}
│     (works whether Owner is a User or a Queue)
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: OwnerId = {!Record.Id})
      → "give me all records owned by this User/Queue"
```

### Queue
```
Queue (Group, Type = Queue)
│
├── Parent
│     └── (none)
│
├── Children
│     └── Queue Members (Users or other Queues assigned to it)
│
├── Up (Child → Parent)
│     ❌ Not applicable
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: OwnerId = {!Record.Id} on Case/Lead → records assigned to this Queue)
```
💡 Used heavily in Service Cloud: unassigned Cases often sit in a Queue
until a support agent picks them up.

### Asset
```
Asset
│
├── Parent
│     ├── Account
│     ├── Contact
│     └── Product2 (the Product this Asset represents)
│
├── Children
│     └── Cases (support issues tied to this specific purchased item)
│
├── Up (Child → Parent)
│     ✅ Direct → {!Record.Account.Name}
│     ✅ Direct → {!Record.Product2.Name}
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: AssetId = {!Record.Id} on Case)
```
💡 An Asset represents something a customer **already owns** after
buying it — this is the bridge between Sales Cloud (the sale) and
Service Cloud (supporting what they bought).

### Order
```
Order
│
├── Parent
│     ├── Account
│     ├── Contract (optional)
│     └── Opportunity (optional, if generated from a won deal)
│
├── Children
│     └── Order Products / OrderItems (Master-Detail)
│
├── Up (Child → Parent)
│     ✅ Direct → {!Record.Account.Name}
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: OrderId = {!Record.Id} on OrderItem)
```

### Contract
```
Contract
│
├── Parent
│     └── Account
│
├── Children
│     └── Orders (Contracts can generate multiple Orders over time)
│
├── Up (Child → Parent)
│     ✅ Direct → {!Record.Account.Name}
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: ContractId = {!Record.Id} on Order)
```

### Campaign
```
Campaign
│
├── Parent
│     └── Parent Campaign (self-relationship, for hierarchies)
│
├── Children
│     └── Campaign Members (Junction Object → Lead OR Contact)
│
├── Up (Child → Parent)
│     ✅ Direct → {!Record.Parent.Name}
│
└── Down (Parent → Child)
      ✅ Get Records + Loop
      (filter: CampaignId = {!Record.Id} on CampaignMember)
```

### Junction Objects (beyond Opportunity Product)
```
CampaignMember   →  connects Campaign ↔ (Lead OR Contact)
AccountContactRelation → connects Account ↔ Contact (many-to-many, e.g.
                          one Contact working with two different Accounts)
```
```
CampaignMember
│
├── Parent
│     ├── Campaign
│     └── Lead OR Contact (polymorphic-like: only one is filled per row)
│
├── Children
│     └── (none)
│
├── Up (Child → Parent)
│     ✅ Direct → {!Record.Campaign.Name}
│     ✅ Direct → {!Record.Lead.Name} (or {!Record.Contact.Name})
│
└── Down (Parent → Child)
      ❌ Not applicable (CampaignMember is already the bottom of the chain)
```
💡 Same logic as [[Opportunity Product]] — any time you see "one Object
can relate to MANY of another, and vice versa," expect a Junction Object
sitting in between with the SAME Up/Down rules as everything else.

---
### 🔗 Related Notes
[[Object Relationship Traversal 1]] | [[Master Schema Map]] | [[Lookup Relationship]] | [[Master-Detail]] | [[Junction Object]] | [[Flow]]
