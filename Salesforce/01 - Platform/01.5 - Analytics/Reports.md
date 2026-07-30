---
tags: [salesforce, platform, concept]
aliases: [Report]
---

# 📊 Reports

## 📌 Definition
**Report** = a list of records from one or more [[Objects]], filtered, grouped, and summarized to answer a business question.
(قائمة سجلات مأخوذة من Object أو أكثر، مُصفّاة ومُجمّعة للإجابة عن سؤال عمل معين)

> A Report doesn't create or change data — it only **reads and displays** it.
(لا ينشئ أو يغيّر بيانات، فقط يعرضها)

## 🧠 Core Idea
A Report answers questions like:
- How many Opportunities are open right now? (كم عدد الصفقات المفتوحة؟)
- Which Leads converted this month? (أي الـ Leads تم تحويلها هذا الشهر؟)
- What's the total Amount of Closed Won deals this quarter?

## 🧾 Report Types
| Type | Description |
|---|---|
| **Tabular** | Simple list, like a spreadsheet — good for exporting data |
| **Summary** | Grouped rows with subtotals (e.g. Opportunities grouped by Stage) |
| **Matrix** | Grouped by rows **and** columns (e.g. Sales Rep × Month) |
| **Joined** | Combines multiple report types/objects in one view |

## 💡 Real Example
```
Report: "Open Opportunities by Stage"

Source Object: Opportunity
Filter: Stage != "Closed Won" AND Stage != "Closed Lost"
Group By: Stage

Result:
Prospecting     → 12 deals, $340,000
Qualification   → 8 deals,  $210,000
Proposal        → 5 deals,  $150,000
Negotiation     → 3 deals,  $90,000
```
(هذا هو بالضبط ما يستخدمه الـ Sales Manager لمعرفة قيمة الصفقات المفتوحة)

## 🧾 Key Elements of a Report
| Element | Purpose |
|---|---|
| Report Type | Which Object(s) the data comes from |
| Filters | Narrow down which records show (e.g. Stage, Date range) |
| Columns | Which fields to display |
| Grouping | Organize rows by a field (e.g. group by Stage or Owner) |
| Summary Fields | Sum, Average, Max, Min of a numeric field |

## ⚖️ Report vs Dashboard
| | Report | [[Dashboards]] |
|---|---|---|
| Format | Table of data (rows & columns) | Visual charts/graphs |
| Purpose | Detailed, precise numbers | Quick visual overview |
| Built from | One or more Objects directly | Built **from Reports** |

(الـ Report يعطي تفاصيل دقيقة، بينما الـ Dashboard يعطي نظرة سريعة بصرية، ويُبنى أصلًا من الـ Reports)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Objects]] | Every Report pulls data from one or more Objects |
| [[Fields]] | Report columns and filters are based on Fields |
| [[Dashboards]] | Dashboards are built by visualizing one or more Reports |

## ❓ Rule to Remember
> Report = a **filtered, grouped list** of records (قائمة مُصفّاة ومُجمّعة)
> Read-only — never modifies data.
> The foundation that [[Dashboards]] are built on top of.

---
### 🔗 Related Notes
[[Objects]] | [[Fields]] | [[Dashboards]] | [[Opportunity]]
