---
tags: [salesforce, platform, concept, environment]
aliases: [Sandbox, Sandbox Org]
---

# 🏖️ Sandboxes

## 📌 Definition
**Sandbox** = a separate, isolated copy of your Salesforce org used for **building, testing, and training** — completely separate from real, live business data.
(نسخة منفصلة ومعزولة من الـ Org، تُستخدم للبناء والاختبار والتدريب، بمعزل تام عن البيانات الحقيقية الحية)

> Nothing you do in a Sandbox affects **Production** (the real, live org customers and employees use).
(أي شيء تفعله في الـ Sandbox لا يؤثر إطلاقًا على الـ Production)

## 🧠 Core Idea
A Sandbox answers: **"Can I try this change safely, without risking real customer data or breaking something live?"**
(هل يمكنني تجربة هذا التغيير بأمان، دون المخاطرة بالبيانات الحقيقية أو كسر شيء مباشر؟)

## 🧾 Types of Sandboxes
| Type | Contains | Best For |
|---|---|---|
| **Developer** | Metadata only (no real data), small storage | Quick coding/config tests |
| **Developer Pro** | Metadata only, larger storage | Slightly bigger dev/test projects |
| **Partial Copy** | Metadata + a **sample** of real data | Realistic testing with limited data |
| **Full Copy** | Metadata + **ALL** real data (exact copy of Production) | Full-scale testing, staging before major releases |

(كلما زاد النوع، زادت كمية البيانات الحقيقية المنسوخة، وزاد الوقت اللازم لإنشائه)

## 💡 Real Example
```
Admin wants to test a new Validation Rule + Flow on Opportunity
before rolling it out to the whole Sales team.

1. Create/refresh a "Partial Copy" Sandbox
2. Build and test the Validation Rule + Flow there
3. Confirm it works as expected with sample data
4. Migrate the change to Production using Change Sets
```
(الـ Admin يبني ويختبر التغيير في Sandbox أولاً، قبل نقله إلى Production)

## ⚠️ Why Never Build Directly in Production?
| Risk | Why Sandbox Prevents It |
|---|---|
| Broken Validation Rule blocks real Sales Reps from saving | Tested safely first in Sandbox |
| A Flow bug creates wrong data for real customers | Caught during Sandbox testing |
| Untested Approval Process locks real deals | Verified in Sandbox before going live |

(بناء تغييرات غير مُختبرة مباشرة في Production قد يعطّل عمل الفريق الحقيقي)

## 🔗 Relation to Other Concepts
| Concept | Relation |
|---|---|
| [[Change Sets]] | The tool used to move tested changes FROM a Sandbox INTO Production |
| [[Flow]] | New/updated Flows should be built and tested in Sandbox first |
| [[Validation Rules]] | Should be tested in Sandbox to avoid blocking real users unexpectedly |
| [[Approval Process]] | Complex approval chains should be verified in Sandbox before deployment |

## ❓ Rule to Remember
> Sandbox = **safe copy of your org** for building & testing (نسخة آمنة للبناء والاختبار)
> Four types: Developer, Developer Pro, Partial Copy, Full Copy — differ by data volume and storage size.
> Never test risky changes (Validation Rules, Flows, Approval Processes) directly in Production.
> Once tested, changes move to Production via [[Change Sets]].

---
### 🔗 Related Notes
[[Change Sets]] | [[Flow]] | [[Validation Rules]] | [[Approval Process]]
