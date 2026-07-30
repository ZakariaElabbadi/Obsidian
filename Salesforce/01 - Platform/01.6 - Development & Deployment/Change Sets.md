---
tags: [salesforce, platform, concept, environment]
aliases: [Change Set]
---

# 📦 Change Sets

## 📌 Definition
**Change Set** = a package of configuration changes (metadata) moved from one Salesforce environment to another — most commonly from a [[Sandboxes|Sandbox]] into Production.
(حزمة من التعديلات (Metadata) تُنقل من بيئة إلى أخرى، غالبًا من Sandbox إلى Production)

> A Change Set moves the **structure/setup** (Objects, Fields, Flows...), not the actual data/records.
(ينقل البنية والإعدادات، وليس السجلات أو البيانات الفعلية)

## 🧠 Core Idea
A Change Set answers: **"I built and tested this in Sandbox — how do I safely bring it into the real, live org?"**
(بنيت واختبرت هذا في Sandbox، كيف أنقله بأمان إلى الـ Org الحقيقي؟)

## 🧾 What Can Be Included in a Change Set
| Component Type | Example |
|---|---|
| [[Objects]] | A new Custom Object, e.g. `Warranty__c` |
| [[Fields]] | A new field added to Opportunity |
| [[Flow]] | A newly built or updated Flow |
| [[Validation Rules]] | A new rule tested in Sandbox |
| [[Page Layouts]] | Updated layout with new fields arranged |
| [[Profiles]] / [[Permission Sets]] | Permission updates (limited support) |
| Reports & Dashboards folders | Shared reporting assets |

## 💡 Real Example — Full Journey
```
1. Admin builds a new Validation Rule + Flow in a "Partial Copy" Sandbox
2. Tests it thoroughly with sample data
3. Creates an "Outbound Change Set" in the Sandbox
4. Adds the Validation Rule + Flow as components
5. Uploads the Change Set to Production
6. In Production, Admin creates an "Inbound Change Set" and clicks Deploy
7. The Validation Rule + Flow now exist in the live org
```
(بعد الاختبار في Sandbox، يُرفع التغيير كـ Change Set ليتم نشره في Production)

## ⚠️ Important Rules About Change Sets
| Rule | Why It Matters |
|---|---|
| Source and target orgs must be **connected** (e.g. Sandbox linked to its Production) | You can't send a Change Set to a random unrelated org |
| Change Sets move **metadata**, not records/data | Use [[Import & Export]] or Data Loader for actual data |
| Some dependencies must be included together | e.g. a Flow using a custom Field requires that Field in the same Change Set |
| Deployment can fail if dependencies are missing | Always review "Validate" results before deploying |

(الـ Change Set ينقل الإعدادات وليس البيانات، ولهذا يُستخدم Import & Export لنقل السجلات)

## ⚖️ Change Set vs Other Deployment Tools
| Tool | Best For |
|---|---|
| **Change Set** | Simple, UI-based deployments between connected orgs (Sandbox ↔ Production) |
| **Metadata API / CLI tools** | Advanced developers, version control (Git), CI/CD pipelines |
| **Unmanaged/Managed Packages** | Distributing reusable functionality across unrelated orgs |

(Change Set مناسب للنقل البسيط عبر الواجهة، بينما الأدوات المتقدمة تُستخدم في مشاريع التطوير الكبيرة)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Sandboxes]] | Change Sets are the standard way to move tested work OUT of a Sandbox |
| [[Flow]] | Newly built Flows are commonly deployed via Change Sets |
| [[Import & Export]] | Handles actual record data — Change Sets handle configuration only |

## ❓ Rule to Remember
> Change Set = **moves metadata/configuration** between connected orgs (ينقل الإعدادات، وليس البيانات)
> Typical path: build & test in [[Sandboxes|Sandbox]] → package as Change Set → deploy to Production.
> Does NOT move actual records — use [[Import & Export]] for that.

---
### 🔗 Related Notes
[[Sandboxes]] | [[Objects]] | [[Fields]] | [[Flow]] | [[Import & Export]]
