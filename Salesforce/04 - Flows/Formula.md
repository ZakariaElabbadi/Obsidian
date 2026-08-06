---
tags: [salesforce, admin, flow, formula]
title: Salesforce Flow - Formula Summary
last_updated: 2026-08-05
---

# Salesforce Flow - Formula Summary

## 🎯 What is a Formula?

A Formula is a resource that **calculates or returns a value** during Flow execution.

It can return:
- Text
- Number
- Boolean
- Date
- Date/Time

> Formula **does not modify records**. It only returns a value — and it's **recalculated every time it's referenced**, never stored.

---

# Where Formulas Are Used

A Formula resource isn't tied to one element — it can be referenced anywhere a value is needed:
- **Decision** conditions
- **Assignment** values
- Default values for **Variables**
- **Screen** component visibility/values
- Inside another **Formula** (formulas can reference other formulas)

---

# Formula vs Assignment

## Formula
- Calculates a value
- Read-only
- Cannot change variables
- Used inside resources

```text
IF({!$Record.Amount} > 1000, "VIP", "Standard")
```

## Assignment
- Stores values
- Modifies Variables
- Modifies Record Variables
- Modifies Collections

```text
TaskRecord.Subject = "Welcome Customer"
```

---

# Operators (Arithmetic & Text)

Before the functions below, remember formulas also support plain operators:

| Operator | Use |
|---|---|
| `+ - * /` | Arithmetic on Number/Currency |
| `&` | Concatenate text, e.g. `{!$Record.FirstName} & " " & {!$Record.LastName}` |
| `= != > < >= <=` | Comparisons (used inside IF/AND/OR/CASE) |
| `( )` | Control order of operations — always parenthesize when mixing AND/OR |

---

# IF()

Returns one value if condition is TRUE and another if FALSE.

```text
IF(condition, value_if_true, value_if_false)
```
```text
IF(
    {!$Record.Amount} >= 10000,
    "VIP",
    "Standard"
)
```

---

# AND()

Returns TRUE if **every** condition is TRUE.

```text
AND(
    {!$Record.Amount} >= 10000,
    {!$Record.Probability} >= 80
)
```

# OR()

Returns TRUE if **at least one** condition is TRUE.

```text
OR(
    {!$Record.Priority} = "High",
    {!$Record.Status} = "Escalated"
)
```

# NOT()

Reverses TRUE and FALSE.

```text
NOT(
    ISBLANK({!$Record.Email})
)
```

---

# ISBLANK()

Checks whether a field is empty. Returns TRUE / FALSE.

```text
ISBLANK({!$Record.Phone})
```
```text
IF(
    ISBLANK({!$Record.Email}),
    "Missing Email",
    "Email OK"
)
```

> ⚠️ **Nuance:** `ISBLANK()` treats an empty string `""` and a truly null field the same way (both = blank). But it does **not** treat `0` as blank for Number fields — `ISBLANK()` on a Number field that's literally `0` returns **FALSE**. Don't use `ISBLANK()` when you actually mean "is zero."

# BLANKVALUE()

Returns a fallback value if a field is blank, otherwise returns the field's actual value — useful to avoid `ISBLANK` + `IF` combos when you just need a default.

```text
BLANKVALUE({!$Record.Description}, "No description provided")
```

---

# ISPICKVAL()

Used only with Picklist fields.

```text
ISPICKVAL(PicklistField, "Value")
```
```text
ISPICKVAL(
    {!$Record.StageName},
    "Closed Won"
)
```

---

# ISNUMBER()

Checks whether a **Text** value can be interpreted as a number — useful before running `VALUE()` on user-entered text to avoid a runtime error.

```text
IF(
    ISNUMBER({!varUserInput}),
    VALUE({!varUserInput}),
    0
)
```

---

# TEXT()

Converts a value into Text. Used with: Number, Picklist, Percent, Date (when needed).

```text
TEXT({!$Record.Amount})
TEXT({!$Record.StageName})
```

> Do **NOT** use with Text fields.
> ❌ `TEXT({!$Record.Name})` — Wrong (Name is already text)
> ✅ `{!$Record.Name}` — Correct

---

# CASE()

Alternative to multiple IF statements. Best when comparing **one field against many fixed values**.

```text
CASE(
Value,
Compare1, Result1,
Compare2, Result2,
DefaultResult
)
```
```text
CASE(
TEXT({!$Record.Status}),
"New","Open Ticket",
"Working","Agent Working",
"Closed","Resolved",
"Unknown Status"
)
```

---

# Text Functions

## LEN()
Returns the number of characters.
```text
LEN({!$Record.FirstName})
```
```text
IF(LEN({!$Record.FirstName}) < 3, "Name Too Short", "Valid Name")
```

## LEFT() / RIGHT() / MID()
```text
LEFT("Salesforce", 5)   → "Sales"
RIGHT("Zakaria", 3)     → "ria"
MID("Zakaria", 3, 4)    → "kari"
```

## CONTAINS()
Checks if one text value contains another — useful for keyword matching.
```text
CONTAINS({!$Record.Description}, "urgent")
```

## FIND()
Returns the position (index) where a substring first appears; returns 0 if not found.
```text
FIND("@", {!$Record.Email})
```

## SUBSTITUTE()
Replaces occurrences of a substring with another value.
```text
SUBSTITUTE({!$Record.Phone}, "-", "")
```

## UPPER() / LOWER() / TRIM()
```text
UPPER("zakaria")         → "ZAKARIA"
LOWER("ZAKARIA")         → "zakaria"
TRIM("   Zakaria   ")    → "Zakaria"
```

> ⚠️ Text comparisons (`=`, `CONTAINS`, `CASE`) are **case-sensitive** by default in most contexts — `"vip"` ≠ `"VIP"`. Normalize with `UPPER()`/`LOWER()` before comparing if the case isn't guaranteed.

---

# Number Functions

## VALUE()
Converts Text into Number.
```text
VALUE("1500")            → 1500
VALUE({!Discount}) + 10
```

## ROUND()
```text
ROUND(12.456, 2)         → 12.46
```

---

# Date Functions

## TODAY()
```text
TODAY()
TODAY() + 30
```

## NOW()
Returns current date and time.
```text
NOW()
```

---

# When to Use Each Function

| Need | Function |
|---|---|
| Evaluate a condition | `IF()` |
| One field vs. many fixed values | `CASE()` |
| Convert Number/Picklist/Percent → Text | `TEXT()` |
| Compare a Picklist value | `ISPICKVAL()` |
| Check an empty field | `ISBLANK()` |
| Default value if blank | `BLANKVALUE()` |
| Validate text is numeric | `ISNUMBER()` |
| Validate text length | `LEN()` |
| Extract beginning / end / middle of text | `LEFT()` / `RIGHT()` / `MID()` |
| Check if text contains a keyword | `CONTAINS()` |
| Find position of a substring | `FIND()` |
| Replace part of a string | `SUBSTITUTE()` |
| Convert case | `UPPER()` / `LOWER()` |
| Remove extra spaces | `TRIM()` |
| Convert Text → Number | `VALUE()` |
| Round a decimal | `ROUND()` |
| Current date / date+time | `TODAY()` / `NOW()` |

---

# Formula Decision Tree

```
Need a condition?              → IF()
Need multiple conditions?      → AND() / OR()
Need opposite result?          → NOT()
Need to compare Picklist?      → ISPICKVAL()
One field vs many values?      → CASE()
Need to check empty field?     → ISBLANK() / BLANKVALUE()
Need to validate numeric text? → ISNUMBER()
Need Text length?              → LEN()
Need beginning of text?        → LEFT()
Need end of text?              → RIGHT()
Need middle of text?           → MID()
Need to find a keyword?        → CONTAINS() / FIND()
Need to replace text?          → SUBSTITUTE()
Need uppercase / lowercase?    → UPPER() / LOWER()
Need remove spaces?            → TRIM()
Need Text → Number?            → VALUE()
Need rounding?                 → ROUND()
Need current date?             → TODAY()
Need current date/time?        → NOW()
```

---

# ✅ Best Practices

- Prefer a **Formula resource** over stacking multiple Decision outcomes when the logic is just a calculation or a single reusable condition — it's cleaner and reusable across multiple elements.
- Wrap mixed `AND()`/`OR()` logic in parentheses explicitly, even when not strictly required, so the precedence is obvious to the next person reading it.
- Normalize case with `UPPER()`/`LOWER()` before text comparisons unless you're certain of the exact casing.
- Use `BLANKVALUE()` instead of `IF(ISBLANK(...), default, field)` — shorter and clearer for simple fallback cases.
- Use `CASE()` instead of a long chain of nested `IF()`s once you're comparing the same field against 3+ fixed values.

# ❌ Common Mistakes

- Using `TEXT()` on a field that's already Text.
- Using `ISBLANK()` on a Number field expecting it to catch `0` — it won't.
- Comparing text values without normalizing case, causing "matches" to silently fail.
- Running `VALUE()` on user-entered text without checking `ISNUMBER()` first — causes a runtime error on non-numeric input.
- Forgetting formulas are **recalculated on every reference**, not cached — don't assume a formula's value "updates" a variable; it doesn't store anything on its own.

---

# 📋 Formula Mastery Checklist

- [x] IF
- [x] AND
- [x] OR
- [x] NOT
- [x] ISBLANK
- [x] BLANKVALUE
- [x] ISPICKVAL
- [x] ISNUMBER
- [x] TEXT
- [x] CASE
- [x] LEN
- [x] LEFT
- [x] RIGHT
- [x] MID
- [x] CONTAINS
- [x] FIND
- [x] SUBSTITUTE
- [x] UPPER
- [x] LOWER
- [x] TRIM
- [x] VALUE
- [x] ROUND
- [x] TODAY
- [x] NOW

## Status
✅ Formula Fundamentals Completed
