---
tags: [salesforce, admin, flow, variables]
title: Variables - Quick Reference
status: Completed
---

# Salesforce Flow - Variables

## 🎯 What is a Variable?

A Variable is a resource that stores data during Flow execution.

Variables exist **only while the Flow is running** — nothing persists unless written out via Create/Update Records.

---

# 📦 Variable Types

## Text
Stores text.
```
Welcome Customer
```
**Use Cases:** Subject, Description, Email, Names

---

## Number
Stores numeric values.

**Operators:** Equals, Add, Subtract, Multiply, Divide

```
varCounter
0
  ↓ Add 1
```

**Use Cases:** Count records, Total Amount, Discounts, Statistics

---

## Currency
Stores monetary amounts, tied to your org's currency/decimal settings (distinct from a plain Number — use Currency whenever the value represents money, e.g. an Opportunity Amount, so formatting and precision stay consistent).

---

## Boolean
Stores only: `True` / `False`

**Use Cases:** Is VIP, Has Manager, Validation

---

## Date
Stores only a date.
```
2026-08-05
```

## DateTime
Stores date and time.
```
2026-08-05 14:30
```

---

## Picklist / Multi-Select Picklist
Stores a value (or values) restricted to a picklist field's defined options — useful when a Decision or Assignment needs to work with a field like Stage or Status without hardcoding free text.

---

## Record Variable
Stores **ONE** Salesforce record.
```
Task
```
**Use Cases:** Assignment, Create Records, Update Records, Subflow

**Create Records:** *"Use all values from a record"*

---

## Record Collection Variable
Stores **MANY** records.
```
Contacts / Tasks / Cases
```
**Use Cases:** Loop, Bulk Update, Bulk Create

**Create/Update Records:** *"Use IDs and all field values from a record collection"*

---

# 🧩 Variable vs Other Resource Types

Variables aren't the only kind of resource in Flow — it's easy to reach for a Variable when a different resource fits better:

| Resource | Can change during the Flow? | Typical use |
|---|---|---|
| **Variable** | ✅ Yes | Values that change as the Flow runs (counters, fetched records, flags) |
| **Formula** | ❌ No (calculated once when referenced) | Derived values, e.g. `Amount * 0.1` or concatenating a name |
| **Constant** | ❌ No (fixed for the whole Flow) | A value that never changes, e.g. a fixed discount rate or a status label |
| **Text Template** | ❌ No (static text with merge fields) | Building an email body or notification message with `{!varName}` merge fields |

> If a value never needs to change once set, a **Constant** or **Formula** is clearer and easier to maintain than a Variable you never reassign.

---

# ⚙️ Variable Configuration Options

When creating any variable, two checkboxes matter:

- **Available for input** — lets the value be set from *outside* the Flow (e.g., passed in from a Screen Flow's launching record, or from a parent Flow calling this one as a subflow).
- **Available for output** — lets this variable's final value be read *after* the Flow finishes (e.g., returned to a parent Flow, or used by a Screen Flow's next screen).

> A variable used only internally (like a loop counter) needs **neither** checked.

---

# 🔤 Naming Convention

- Prefix with `var` for plain variables (`varCounter`, `varIsVIP`).
- Prefix Record Variables with the object name for clarity (e.g., `recTask`, `recAccount`).
- Prefix Collections to make plurality obvious (`colContacts`, `colTasksToCreate`).

---

# Assignment (Modifying Variables)

Assignment modifies data inside the Flow.

**Operators:** Equals, Add, Subtract, Add to Collection, Remove from Collection

```
varCounter += 1
```
```
Loop_Contact.Department = Sales
```

---

# Variable vs Record

**Variable**
```
varCounter = 5
```

**Record (field reference)**
```
Task.Subject
Contact.Department
```

---

# Record Variable Workflow

```
Assignment
   ↓
Fill Record Variable
   ↓
Create Records
   ↓
Use all values from a record
```

# Record Collection Workflow

```
Loop
   ↓
Assignment
   ↓
Add Record
   ↓
Record Collection
   ↓
Create / Update Records
```

---

# Number Variable Example

```
varCounter = 0
Loop
  ↓
Add 1
  ↓
After Last
  ↓
Decision
```

# Boolean Example

```
Decision
  ↓
Assignment: varIsVIP = True
  ↓
Decision: varIsVIP == True
```

---

# ✅ Best Practices

- Use Record Variables for **one** record.
- Use Record Collection Variables for **many** records.
- Use Assignment to prepare data before Create Records.
- Bulk Update/Create **after** the Loop, not inside it.
- Use a **Constant** or **Formula** instead of a Variable for values that never change.
- Only check "Available for input/output" when the variable actually needs to cross the Flow's boundary (subflow, Screen Flow).
- Follow a consistent naming convention (`var`, `rec`, `col` prefixes) so resource type is obvious at a glance.

# ❌ Common Mistakes

- Never Update Records inside a Loop unless truly necessary.
- Never Create Records inside a Loop when bulk processing is possible.
- Using a Variable for a value that's actually constant — makes the Flow harder to audit (was it ever reassigned somewhere?).
- Leaving "Available for output" unchecked on a variable a parent Flow actually needs back from a subflow — the calling Flow gets nothing.
- Confusing a Record Variable (single record, e.g. `Task`) with a Record Collection Variable (multiple records, e.g. `Tasks`) — they aren't interchangeable in Create/Update Records configuration.

---

# 📚 Skills Learned

- Text / Number / Currency / Boolean / Date / DateTime / Picklist Variables
- Record Variables & Record Collection Variables
- Assignment
- Variable vs Formula vs Constant vs Text Template
- Input/Output availability
- Bulk Processing
- Loop Integration
- Decision Integration
