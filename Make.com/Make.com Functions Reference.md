---
tags: [make.com, automation, functions, integromat]
title: Make.com Functions Reference
source: https://help.make.com/functions
---

# Make.com Functions Reference

> Compiled directly from the official docs (help.make.com/functions and its sub-pages). Functions work like Excel formulas — inserted into any field's mapping panel, grouped into tabs: **General, Math, Text & Binary, Date & Time, Array, Custom.**

## 📑 Table of Contents
1. [[#1. Where Functions Live]]
2. [[#2. General Functions]]
3. [[#3. Math Functions]]
4. [[#4. Math Variables]]
5. [[#5. Text and Binary Functions]]
6. [[#6. Date and Time Functions]]
7. [[#7. Array Functions]]
8. [[#8. Custom Functions (JavaScript)]]
9. [[#9. Handy Combined Formulas]]
10. [[#10. Resources]]

---

## 1. Where Functions Live

Click any module field → the mapping panel opens. The first tab shows items from previous modules; the rest are function tabs: **General · Math · Text & Binary · Date & Time · Array · Custom**. Functions are written `functionname(arg1; arg2; ...)` — arguments separated by **semicolons**, not commas.

---

## 2. General Functions

Fine-tune mapping logic — select/omit items from arrays or objects, apply conditions.

| Function | Syntax | What it does | Example |
|---|---|---|---|
| `equal` | `equal(value; value)` | Compares two values for equality | — |
| `set` | `set(object; path; value)` | Sets/adds a value at a location in an array or object, leaving the rest unchanged | `set(user; name; John)` → sets `name`. `set(user; address.city; Prague)` → nested via dot notation |
| `get` | `get(object or array; path)` | Returns the value at a path; nested objects use dot notation; **first array item = index 1** | `get(array; 1)`, `get(object; raw_name)` |
| `if` | `if(expression; value1; value2)` | Returns value1 if expression is TRUE, else value2 | `if(1=1; a; b)` → `a` |
| `ifempty` | `ifempty(value1; value2)` | Returns value1 if not empty, else value2 | `ifempty(a; b)` → `a`; `ifempty(""; b)` → `b` |
| `switch` | `switch(expression; value1; result1; [value2; result2]; [else])` | Compares expression against a list of values, returns the matching result | `switch(b; a;1; b;2; c;3)` → `2` |
| `omit` | `omit(collection; key1; [key2])` | Removes given keys from a collection — useful to strip fields before sending to an API | — |
| `pick` | `pick(collection; key1; [key2])` | Keeps **only** the given keys from a collection | — |

**Keyword: `erase`** — the "erase" pill inherits the type of the item it replaces: a string/number → `null`, an array → `[]`, a collection → `{}`. Use it to explicitly clear a field's value.

---

## 3. Math Functions

Perform calculations, rounding, and number formatting.

| Function | Syntax | What it does | Example |
|---|---|---|---|
| `abs` | `abs(number)` | Absolute value | `abs(-5)` → `5` |
| `average` | `average([array])` or `average(v1; v2; ...)` | Average of values | — |
| `ceil` | `ceil(number)` | Smallest integer ≥ number | `ceil(1.2)` → `2` |
| `floor` | `floor(number)` | Largest integer ≤ number | `floor(1.9)` → `1` |
| `formatnumber` | `formatnumber(number; decimalpoints; [decimalseparator]; [thousandsseparator])` | Formats a number (default decimal `,`, thousands sep ` `) | `formatnumber(123456789; 3; ,; .)` → `123.456.789,000` |
| `max` | `max([array])` or `max(v1; v2; ...)` | Largest number | — |
| `median` | `median([array])` | Median value | `median(3;5;7)` → `5` |
| `min` | `min([array])` or `min(v1; v2; ...)` | Smallest number | — |
| `parsenumber` | `parsenumber(text; decimal_separator)` | Parses a numeric string into a number | `parsenumber("1.756,456"; ,)` |
| `round` | `round(number)` | Rounds to nearest integer | `round(1.5)` → `2` |
| `stdevp` | `stdevp([array])` | Standard deviation, **population** | — |
| `stdevs` | `stdevs([array])` | Standard deviation, **sample** | — |
| `sum` | `sum([array])` or `sum(v1; v2; ...)` | Sum of values | — |
| `trunc` | `trunc(number; [decimals])` | Truncates (removes) the fractional part | `trunc(3.789)` → `3`; `trunc(3.789; 2)` → `3.78` |

---

## 4. Math Variables

| Variable | What it does |
|---|---|
| `random` | Returns a pseudo-random float in `[0, 1)` |

**Generate a random integer in `[min, max]` (inclusive both ends):**
```
{{floor(random * (max - min + 1)) + min}}
```
**Example — roll a 6-sided die:**
```
{{floor(random * 6) + 1}}
```

---

## 5. Text and Binary Functions

Modify/transform text; encode/decode binary data.

| Function | Syntax | What it does | Example |
|---|---|---|---|
| `ascii` | `ascii(text; [remove_diacritics])` | Removes non-ASCII characters | `ascii("Ěščřž"; true)` → `escrz` |
| `base64` | `base64(text)` | Encodes text to Base64 | `base64("Make")` → `TWFrZQ==` |
| `capitalize` | `capitalize(text)` | Uppercases first character only | `capitalize("make")` → `Make` |
| `contains` | `contains(text; search_string)` | Checks if text contains a substring | `contains("hello world"; "hello")` → `true` |
| `decodeurl` | `decodeurl(text)` | Decodes URL-encoded text | `decodeurl("automate%20your%20workflow")` → `automate your workflow` |
| `encodeurl` | `encodeurl(text)` | Encodes text into a URL-safe string | — |
| `escapehtml` | `escapehtml(text)` | Escapes HTML tags | `escapehtml("<b>hi</b>")` → `&lt;b&gt;hi&lt;/b&gt;` |
| `escapejson` | `escapejson(text)` | Escapes quotes/backslashes for safe JSON embedding | — |
| `escapemarkdown` | `escapemarkdown(text)` | Escapes Markdown tags | `escapemarkdown("# header")` → `\# header` |
| `indexof` | `indexof(string; value; [start])` | Position of first occurrence; `-1` if not found | `indexof("make"; "k")` → `2` |
| `length` | `length(text or buffer)` | Character count (text) or byte size (binary) | `length("hello")` → `5` |
| `lower` | `lower(text)` | Lowercases all characters | — |
| `md5` | `md5(text)` | MD5 hash of a string | — |
| `replace` | `replace(text; search_string; replacement)` | Replaces occurrences; supports **regex** in `/pattern/flags` form | `replace("hello world"; "hello"; "hi")` → `hi world` |
| `replaceemojicharacters` | `replaceemojicharacters(text)` | Replaces emoji characters | — |
| `sha1` / `sha256` / `sha512` | `sha1(text; [encoding]; [key])` etc. | Hash function; returns HMAC hash if a `key` is given. Encodings: `hex` (default), `base64`, `latin1` | — |
| `split` | `split(text; separator)` | Splits text into an array | `split("john,george,paul"; ",")` |
| `startcase` | `startcase(text)` | Capitalizes first letter of every word | `startcase("hello world")` → `Hello World` |
| `striphtml` | `striphtml(text)` | Removes all HTML tags | `striphtml("<b>hello</b>")` → `hello` |
| `substring` | `substring(text; start; end)` | Portion of text between positions | `substring("hello"; 0; 3)` → `hel` |
| `tobinary` | `tobinary(value; [encoding])` | Converts a value to binary data (optionally from hex/base64) | — |
| `tostring` | `tostring(value)` | Converts any value to a string | — |
| `trim` | `trim(text)` | Removes leading/trailing spaces | — |
| `upper` | `upper(text)` | Uppercases all characters | — |

> **Regex tip:** `replace()` supports capture groups in the replacement string — `$&` inserts the whole match, `$1`, `$2`... insert numbered capture groups. **Named** capture groups (`?<name>`) are **not** supported in the replacement argument and will error.

---

## 6. Date and Time Functions

Convert, parse, and calculate dates/times, with timezone support.

| Function | Syntax | What it does |
|---|---|---|
| `formatdate` | `formatdate(date; format; [timezone])` | Converts a **date value → text**, using format tokens. If timezone omitted, uses the org's timezone. |
| `parsedate` | `parsedate(text; format; [timezone])` | Converts **text → date value**, using format tokens |
| `adddays` / `addhours` / `addminutes` / `addmonths` / `addseconds` / `addyears` | `addX(date; number)` | Adds (or, with a negative number, subtracts) a time unit to a date |
| `setsecond` / `setminute` / `sethour` | `setX(date; number)` | Sets that specific unit on a date (out-of-range values roll into the next/prev unit) |
| `setday` | `setday(date; number/day_name)` | Sets the day of the week (1=Sunday...7=Saturday, or e.g. `"monday"`) within the current week |
| `setdate` | `setdate(date; number)` | Sets the day-of-month (1–31; out-of-range rolls into next/prev month) |
| `setmonth` | `setmonth(date; number/month_name)` | Sets the month (1–12 or e.g. `"january"`) |
| `setyear` | `setyear(date; number)` | Sets the year |

**Examples:**
```
formatdate(1.dateCreated; "MM/DD/YYYY")           → 10/01/2018
formatdate(1.dateCreated; "YYYY-MM-DD HH:mm A"; "UTC")
parsedate("2016-12-28"; "YYYY-MM-DD")             → 2016-12-28T00:00:00.000Z
adddays("2016-12-08T15:55:57.536Z"; 2)            → 2016-12-10T15:55:57.536Z
addhours(date; -2)                                → subtracts 2 hours
setday("2018-06-27..."; "monday")                 → nearest Monday in that week
```

> Full token references: [Tokens for date/time parsing](https://help.make.com/tokens-for-datetime-parsing) and [Tokens for date/time formatting](https://help.make.com/tokens-for-datetime-formatting). Common tokens: `YYYY` (4-digit year), `MM` (month), `DD` (day), `HH` (24h hour), `mm` (minutes), `ss` (seconds), `A` (AM/PM).

### 📐 Useful Combined Formulas (from official docs)

**Nth day-of-week in a month** (e.g. 2nd Wednesday of the current month):
```
{{adddays(setdate(1.date;1); (1.n-1)*7 + (1.dow-formatdate(adddays(setdate(1.date;1); "-1"); "E")))}}
```
Where `n` = which occurrence (1st, 2nd...), `dow` = day of week (1=Mon...7=Sun).

**Days between two dates** (values must be `date` type — use `parsedate()` first if they're strings):
```
{{round((2.value - 1.value) / 1000 / 60 / 60 / 24)}}
```
> `round()` compensates for daylight-savings edge cases where a plain division gives a non-integer.

**Last day / last millisecond of the current month:**
```
{{adddays(setdate(now; 1); 1)}}                                  → last day
{{parsedate(parsedate(formatdate(now; "YYYYMM01"); "YYYYMMDD"; "UTC") - 1; "x")}}   → last millisecond
```
> Prefer a **half-open interval** (`start ≤ d < next_month_start`) over closed-interval math when filtering date ranges — simpler and avoids off-by-one errors.

**Convert seconds → H:M:S:**
```
{{floor(1.seconds / 3600)}}                    → hours
{{floor((1.seconds mod 3600) / 60)}}           → minutes
{{(1.seconds mod 3600) mod 60}}                → seconds
```
(Only valid if `seconds` < 86400, i.e. less than a full day.)

---

## 7. Array Functions

Search, sort, transform, and restructure arrays.

| Function | Syntax | What it does | Example |
|---|---|---|---|
| `add` | `add(array; value1; [value2...])` | Adds values to an array | — |
| `arraydiff` | `arraydiff(array1; array2)` | Items in array1 **not** in array2 | `arraydiff([1,2,3,4]; [3,4,5,6])` → `[1,2]` |
| `arrayintersect` | `arrayintersect(array1; array2)` | Items present in **both** arrays | `arrayintersect([1,2,3,4]; [3,4,5,6])` → `[3,4]` |
| `contains` | `contains(array; value)` | Checks if array contains a value | — |
| `deduplicate` | `deduplicate(array)` | Removes duplicate values | — |
| `distinct` | `distinct(array; [key])` | Removes duplicates by comparing a key (for complex objects); dot notation for nested keys | `distinct(contacts[]; name)` |
| `first` | `first(array)` | First element | — |
| `flatten` | `flatten(array)` | Flattens nested sub-arrays into one array | — |
| `join` | `join(array; separator)` | Concatenates array items into a string | — |
| `keys` | `keys(object)` | Array of an object's/array's property names | — |
| `last` | `last(array)` | Last element | — |
| `length` | `length(array)` | Number of items | — |
| `map` | `map(complex_array; key; [filter_key]; [filter_values])` | Extracts a primitive array of values by key, optionally filtered | `map(emails[]; email; label; work,home)` |
| `merge` | `merge(array1; array2; ...)` | Merges multiple arrays into one | — |
| `remove` | `remove(array; value1; [value2...])` | Removes given values (primitive arrays only) | — |
| `reverse` | `reverse(array)` | Reverses element order | — |
| `shuffle` | `shuffle(array)` | Randomly reorders elements | — |
| `slice` | `slice(array; start; [end])` | Returns items in a range (0-indexed) | — |
| `sort` | `sort(array; [order]; [key])` | Sorts an array. Orders: `asc` (default), `desc`, `asc ci`, `desc ci` (case-insensitive) | `sort(contacts[]; desc; name)` |
| `toarray` | `toarray(collection)` | Converts a collection into an array of key-value pairs | — |
| `tocollection` | `tocollection(array; key; value)` | Converts a key-value array into a collection | — |

> ⚠️ **Note the indexing inconsistency:** most array functions treat the **first item as index 1** (e.g. `get()`, `sort` key access), but `slice()` uses **0-based** indexing like most programming languages. Double-check per function.

---

## 8. Custom Functions (JavaScript)

> **Enterprise plans only.** Custom functions extend the built-in transformation library using **JavaScript (ES6)**.

### Rules & Limits
- Created/managed in the **Functions** section (sidebar → Functions, or ⋮ → Functions). Editing requires **Team Admin** role; viewing/using requires **Team Member**.
- Structure: a standard JS function — header (name + params), body in `{}`, exactly **one `return`** statement.
- **No 3rd-party libraries.**
- **No async code** — functions must be **synchronous**.
- **No HTTP requests** from inside a function.
- **Cannot call other custom functions** from within a custom function (no nesting).
- **No recursion.**
- Max runtime: **300 ms** per call.
- Max code length: **5000 characters**.
- Make does **not validate** your code — bugs surface as scenario execution errors, and a scenario using a function you later delete will fail with `Function '<name>' not found!`.
- Dates inside a custom function respect your **organization's timezone**.
- You **can** call Make's own built-in functions from inside custom code via the `iml` object, e.g. `iml.length(text)`.
- To feed a custom-function result into an **Iterator**, first run it through a **Set Variable** module, then map that variable into the Iterator (can't call a custom function directly inside an Iterator).
- Every save creates a **version history** entry — you can compare/restore previous versions.
- Debug via the built-in **Debug Console** under the code editor.

### Examples (from official docs)

**Hello World:**
```js
function helloWorld() {
  return "Hello world!";
}
```

**Count working days in a month:**
```js
function numberOfWorkingDays(month, year) {
  let counter = 0;
  let date = new Date(year, month - 1, 1);
  const endDate = new Date(date.getFullYear(), date.getMonth() + 1, 0);
  while (date.getTime() < endDate.getTime()) {
    const weekday = date.getDay();
    if (weekday !== 0 && weekday !== 6) counter += 1;
    date = new Date(date.getFullYear(), date.getMonth(), date.getDate() + 1);
  }
  return counter;
}
```

**Days between two dates:**
```js
function numberOfDays(start, end) {
  const startDate = new Date(start);
  const endDate = new Date(end);
  return Math.abs((startDate.getTime() - endDate.getTime()) / (1000*60*60*24));
}
```

**Random greeting from an array:**
```js
function randomGreeting(greetings) {
  const index = Math.floor(Math.random() * greetings.length);
  return greetings[index];
}
```

---

## 9. Handy Combined Formulas

| Goal | Formula |
|---|---|
| Random integer in `[min,max]` | `{{floor(random * (max - min + 1)) + min}}` |
| Days between two date values | `{{round((date2 - date1) / 1000 / 60 / 60 / 24)}}` |
| Last day of current month | `{{adddays(setdate(now; 1); -1)}}` |
| Seconds → H/M/S | `floor(s/3600)` · `floor((s mod 3600)/60)` · `(s mod 3600) mod 60` |
| Strip password before sending to API | `omit(collection; "password")` |
| Only keep 2 needed fields for an API call | `pick(collection; "name"; "email")` |
| Default value if a field is blank | `ifempty(field; "N/A")` |

---

## 10. Resources

- [Functions (index)](https://help.make.com/functions)
- [Use functions](https://help.make.com/use-functions)
- [General functions](https://help.make.com/general-functions)
- [Math functions](https://help.make.com/math-functions)
- [Math variables](https://help.make.com/math-variables)
- [Text and binary functions](https://help.make.com/text-and-binary-functions)
- [Date and time functions](https://help.make.com/date-and-time-functions)
- [Tokens for date/time parsing](https://help.make.com/tokens-for-datetime-parsing)
- [Tokens for date/time formatting](https://help.make.com/tokens-for-datetime-formatting)
- [Array functions](https://help.make.com/array-functions)
- [Custom functions](https://help.make.com/custom-functions)
- [Item data types](https://help.make.com/item-data-types)
- [Mapping arrays](https://help.make.com/mapping-arrays)
