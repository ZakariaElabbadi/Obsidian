---
tags: [salesforce, platform, concept]
aliases: [Dashboard]
---

# 📈 Dashboards

## 📌 Definition
**Dashboard** = a **visual** collection of charts and graphs, built from one or more [[Reports]].
(مجموعة بصرية من الرسوم البيانية، مبنية من تقرير أو أكثر)

> A Dashboard shows nothing on its own — it always **visualizes data from a Report**.
(الـ Dashboard لا يعرض شيئًا بمفرده، بل يعتمد دائمًا على بيانات من Report)

## 🧠 Core Idea
A Dashboard answers: **"Can I see the big picture at a glance, without reading rows of numbers?"**
(هل أستطيع رؤية الصورة الكاملة بنظرة سريعة، دون قراءة صفوف من الأرقام؟)

## 🧾 Common Dashboard Components
| Component | Best For |
|---|---|
| Bar Chart | Comparing values across categories (e.g. Opportunities by Stage) |
| Pie Chart | Showing proportions (e.g. % of deals per Sales Rep) |
| Line Chart | Trends over time (e.g. Revenue per month) |
| Gauge | Progress toward a goal (e.g. Quota achieved) |
| Metric | A single big number (e.g. Total Closed Won this quarter) |
| Table | A compact list view |

## 💡 Real Example
```
Dashboard: "Sales Performance Overview"

Component 1 (Bar Chart)  ← from Report "Open Opportunities by Stage"
Component 2 (Gauge)       ← from Report "Quota Achievement"
Component 3 (Pie Chart)   ← from Report "Deals Won by Sales Rep"
```
A Sales Manager opens this Dashboard every Monday morning to instantly see
how the team is performing — without opening multiple Reports individually.
(بدل فتح عدة تقارير منفصلة، يرى المدير كل شيء بنظرة واحدة)

## ⚖️ Dashboard vs Report — Quick Comparison
| | [[Reports|Report]] | Dashboard |
|---|---|---|
| Format | Table of rows & columns | Visual charts |
| Precision | Exact numbers, every row | High-level overview |
| Built from | Objects directly | One or more Reports |
| Best for | Deep analysis | Quick decision-making |

(الـ Report للتحليل الدقيق، الـ Dashboard لاتخاذ قرار سريع بنظرة واحدة)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Reports]] | Every Dashboard component is powered by a Report |
| [[Objects]] | Indirectly connected — Reports pull from Objects, Dashboards visualize Reports |
| [[Profiles]] / [[Permission Sets]] | Control who can view or edit a Dashboard |

## ❓ Rule to Remember
> Dashboard = **visual layer on top of Reports** (طبقة بصرية فوق التقارير)
> Never built directly from Objects — always from Reports.
> Best used for quick, at-a-glance decision-making, not detailed analysis.

---
### 🔗 Related Notes
[[Reports]] | [[Objects]] | [[Fields]] | [[Opportunity]]
