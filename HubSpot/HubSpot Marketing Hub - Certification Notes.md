---
tags: [hubspot, marketing, certification, MOC]
created: 2026-08-03
source: HubSpot Academy Transcripts
---

# 🎯 HubSpot Marketing Hub — Certification Notes (MOC)

> [!info] Map of Content
> This note summarizes 11 HubSpot Academy lesson transcripts covering the Marketing Hub certification. Use the links below to jump to a section.

- [[#1. Introduction to Marketing Hub]]
- [[#2. Exploring the Contacts Database]]
- [[#3. Using Buyer Personas]]
- [[#4. Understanding Segmentation]]
- [[#5. Creating Forms]]
- [[#6. Creating Calls-to-Action (CTAs)]]
- [[#7. Getting Started With Email]]
- [[#8. Understanding Workflows]]
- [[#9. Understanding Social Media]]
- [[#10. Creating a Campaign]]
- [[#11. Understanding Reporting]]

---

## 1. Introduction to Marketing Hub

> [!abstract] What it is
> An all-in-one **marketing automation software** to generate leads and automate marketing that drives growth.

### Core value
- Drive revenue by attracting, nurturing, converting high-quality leads
- Save time via campaign management + automation in one place
- Measure/optimize with reporting powered by CRM data

### Inbound methodology (3 stages)
1. **Attract** → ads, campaigns, social, video
2. **Engage** → forms, CTAs, email, automation
3. **Delight** → live chat, SMS, WhatsApp, Meta Messenger, smart content, A/B testing

### Supporting features
- Lead scoring, behavioral events, segmentation, reporting
- Powered by the **Smart CRM** (shared across Content Hub, Sales Hub, Service Hub, Operations Hub) → single source of truth

### Navigation map
| Menu | Tools |
|---|---|
| CRM | Contacts, Companies, Lists |
| Marketing | Campaigns, Marketing Email, Social, Ads, Forms, CTAs, SMS |
| Automations | Workflows (Pro/Enterprise) |
| Reporting & Data | Reports, Analyze tabs |

#### Quick automation examples
- **New ebook launch** → Facebook lead-gen ad + organic social posts + optimized form (progressive profiling)
- **New feature launch** → Google Search ad + teaser video + email announcement/workflow + CTA + lead scoring + campaign tracking
- **Customer retention** → thank-you emails, loyalty SMS/WhatsApp, abandoned cart automation, review-request workflow

#tags: #marketing-hub #overview

---

## 2. Exploring the Contacts Database

> [!abstract] Why it matters
> The **contacts database (CRM)** is the foundation for personalized relationships at scale and the backbone of every campaign.

### Contact management
Definition: a strategy using software (HubSpot) to **source, store, manage** contact info.

Three key CRM features:
- **Contact records** — retrieve info on anyone the business interacts with
- **Contact properties** — e.g., email, lifecycle stage (auto-populated)
- **Lists** — segment contacts by property values/activities

### Keeping the database healthy
1. **Clean & organized** — database "decays" every year; review quarterly ("When are contacts unengaged? When should we remove them?")
2. **Customize** — build custom properties (contact/company/deal/ticket/product) for personalization

### Lead intelligence
- **Automatic**: page views, social interactions, email engagement
- **Manual/collected**: forms, chatbots, messaging apps, surveys

### How-to steps
- **Access**: `CRM → Contacts` (or `Contacts → Companies`)
- **Manually create contact**: `CRM → Contacts → Create contact` → Email/First/Last name required → optional: owner, job title, phone, lifecycle stage, lead status, marketing contact checkbox
- **Import contacts**: `CRM → Contacts → Import → Start an import` → upload CSV/XLSX/XLS → map columns → optionally create a list from the import → also import **opt-out lists** for consent compliance
- **Custom property**: Settings icon → Data Management → Properties → Create property → set label, object type, group, field type
- **View a contact**: search → click name → Overview tab (recent activity) / Actions → View all properties → associated companies/deals/tickets shown in side cards → Notes/Emails/Calls/Tasks/Meetings available directly on record

#tags: #contacts #crm #data-management

---

## 3. Using Buyer Personas

> [!abstract] Definition
> A **semi-fictional representation** of your ideal customer based on real data + educated speculation about demographics, behavior, motivations, goals.

### Data types
- **Psychographic** — thoughts, opinions, aspirations (interview-based, often more revealing of motivation)
- **Demographic** — age, income, education, location (fact-based)

### ⚠️ Common mistake
> [!warning] Don't confuse personas with job functions
> Group personas by **goal/challenge**, not by title (e.g., not "Sales Manager persona" vs "Sales VP persona").

### Key discovery questions
- B2B: "What does success in your role mean?" / B2C: "What are your goals?"
- "What are your biggest challenges?"
- "What is your job role/title (and who do you report to)?"
- Demographics: age, income, education, location
- "Which publications/blogs do you read?" (great for niche targeting)

### Building in HubSpot
`Settings → Data Management → Properties → search "Persona" → Field type → Add another persona`
Fill in: Name, Description, photo, **Roles/Goals/Challenges** (Internal Notes), Demographics, and an optional narrative story.

> [!tip] Best practice
> Aim for **3–5 personas** max; name them memorably/alliteratively (e.g., "Skeptical Suzy").

#tags: #buyer-personas #strategy

---

## 4. Understanding Segmentation

> [!abstract] Definition
> Separating customers into groups based on shared **traits** (personality, interests, habits) and **factors** (demographics, industry, income).

### Benefits
- Deeper customer understanding → tailored content
- Targeted campaigns/ads
- Better service/support prep
- Increased loyalty
- Channel-preference communication
- Spot new product/service opportunities

### Foundational segments to build
- Lifecycle stage (subscriber/lead/customer) — tracked via the **lifecycle stage property**
- Buyer personas
- Other types: Geographic, Psychographic, Technographic, Behavioral, Needs-Based, Value-Based

### Lists tool = HubSpot's segmentation mechanism
| Type | Behavior | Common use cases |
|---|---|---|
| **Active list** | Dynamic — auto-updates as contacts meet/leave criteria | Ongoing newsletters, lifecycle grouping, HubSpot score segmentation |
| **Static list** | Fixed snapshot — manual add/remove | One-time email blasts, event attendee lists, manual workflow enrollment, bulk delete |

### Where segments are used
- **Workflows** — `Automations → Workflows` → List Membership as enrollment trigger
- **Email** — `Marketing → Email → [draft] → Recipients tab` → select active/static list (saved filters not available here)
- Smart content personalization

### Creating a list
`Contacts → Lists → Create list` (active) or `Contacts → Contacts → add filter → Save filter` (saved filter, contacts dashboard only)

#tags: #segmentation #lists #lifecycle-stage

---

## 5. Creating Forms

> [!abstract] Why forms matter
> 74% of marketers use web forms for lead gen; 49.7% call them their **highest-converting** lead gen tool (per HubSpot research).

### Common form types
- **Contact forms** — questions/concerns/refunds
- **Lead generation forms** — convert visitors to leads
- **Order forms** — payment + shipping/billing (multi-step)
- **Registration forms** — service sign-up
- **Survey forms** — multiple choice/fill-in/long-form feedback

### Form design best practices
- Be **simple** — fewer fields = higher conversion (Imagescape: 11→4 fields = **+120%** conversion rate)
- **Single-column** layout (CXL study: 15.4 sec faster completion)
- Order fields **easiest → hardest**
- **Inline validation** with positive, clear error messages
- Enable **autofill/autocorrect** with recognizable field names
- Use **summary boxes** to address user concerns (e.g., why you need a zip code)
- Design for **mobile** — minimalist, branded, color-coordinated
- Example: one extraneous field cost Expedia **$12M/year** in lost profit

### Building a form (`Marketing → Forms → Create form`)
1. Choose **Embedded form** (site/CTA) or **Standalone page** (shareable link)
2. Pick **Blank template** or a pre-made one (e.g., "Contact us")
3. Drag/drop fields; toggle **Ticket Properties** to auto-create support tickets
4. Toggle **captcha** under "Other form elements"
5. Edit field: required/hidden toggles, Label/Help Text/Placeholder/Default value
6. **Logic tab** (Pro/Enterprise): progressive fields (replace known values) + dependent fields (conditional qualifying questions)
7. **Options tab**: thank-you message or redirect URL; set lifecycle stage; submission notifications; language; campaign association
8. Toggles: always create new contact per email, marketing contact default, reset-form link, pre-populate known values
9. **Style & preview tab** → Style (fonts/colors/width) → Test (preview as a contact w/ progressive fields)
10. Click **Update → Publish** → get embed code or share link

### Embedding as a pop-up (CTA tool)
`Marketing → CTAs → Create → Start from scratch` → choose **Sticky Banner / Pop-Up Box / Slide-In** → drag Form module in → set Design, Layout, Targeting (scroll %, exit intent, elapsed time, inactivity), Options → **Review and publish**

#tags: #forms #lead-generation #conversion

---

## 6. Creating Calls-to-Actions (CTAs)

> [!abstract] Definition
> A CTA is an image or text prompting visitors/leads/customers to take an **action** (download, sign up, get a coupon, attend an event).

### CTA formats
- **Image CTAs** — banner-style with value copy
- **Button CTAs** — clickable, drive to conversion pages
- **Anchor Text CTAs** — hyperlinked text with action verbs ("download," "access")

### Benefits
- Adds interactivity
- Matches content to buyer's-journey stage
- Trackable performance/clicks over time (unlike plain links)

### Best practices
- **Actionable, second-person language**: "Download now," "Start saving now," "Sign me up" (avoid "submit")
- Keep copy **90–150 characters**
- **Align CTA copy with landing page copy** (same offer name/type on both)
- Include a **clear value proposition** (Amazon Music free trial example)
- Create **urgency** — words like "now"/"today"; "Claim Offer" > "Get Offer" (Barkbox example)
- **High contrast design** so it pops (Spotify example: light purple on dark purple)
- Always add **alt text** (SEO + accessibility)
- **Make it big** and placed prominently (above the fold = more clicks; below = higher-quality leads)
- **A/B test** continuously
- **Personalize/Smart CTAs** (Pro/Enterprise) — tailor by location, language, lead/customer status → **202% better performance** than basic CTAs

### Building a CTA button
`Marketing → Lead Capture → CTAs → Create CTA`
- Design tab: button text, style, color, or switch to **Image Button** (upload + alt text + sizing)
- Advanced options: custom CSS, size
- Options tab: internal name; redirect type — **External URL**, **HubSpot page/blog post**, or **Meeting link** (Sales Hub); open in new window option; link to a campaign
- Save → Preview → **Finish**

### Inserting a CTA into content
Rich text/body module → **Insert dropdown → Call-to-Action** (or CTA icon in toolbar) → select by internal name → **Insert**. Templates may also have a dedicated CTA module.

#tags: #cta #conversion #design

---

## 7. Getting Started With Email

> [!abstract] Why email matters
> 77% of marketers saw increased engagement (HubSpot data); 50% of recipients purchase monthly due to email (Salecycle); 99% of users check inbox daily.

### Strategy pillars
Deliverability, segmentation, personalization, automation.

### Email types (`Marketing → Email → Create email`)
| Type | Use |
|---|---|
| **Regular email** | One-time send to a segment |
| **Automated email** | Triggered via workflows; reusable across multiple workflows |
| **Blog/RSS email** | Auto-sent on new blog/RSS content (Pro/Enterprise only) |

### Blog/RSS specifics
- Requires blog selection (internal or external RSS URL)
- Frequency: instant / daily / weekly / monthly (one frequency per blog per contact)
- Choose summary vs. full post; set max # of posts to display

### Email settings
- **From name/address** — supports dynamic tokens (e.g., contact owner)
- **Subject line*** — required; can generate via Breeze AI
- **Personalization tokens** — via "Personalize" button
- **Preview text**
- **Internal email name**, Language, **Subscription type***, optional campaign link

### Performance tracking
`Marketing → Email → [select email] → Performance page`
Metrics: **Open rate, Click rate, Reply rate, Delivery, Revenue Attribution, Top clicked links, Top engaged contacts, Time spent viewing, Engagement over time**

#tags: #email #email-marketing

---

## 8. Understanding Workflows

> [!abstract] Definition
> **Marketing automation** = software that automatically performs routine marketing tasks. HubSpot's primary tool = **Workflows** (Pro/Enterprise only).

### Why automate
- Lead nurturing at scale without losing human touch
- Internal team communication (notify sales/contact owners)
- Data hygiene (remove unengaged contacts automatically)

### Building a workflow
`Automations → Workflows → Create workflow` → **From template** (recommended for beginners; filter by plan/objective) or **From scratch** (Contact-based / Company-based for marketing)

### Enrollment trigger types
| Trigger | Behavior |
|---|---|
| **Event-based** | Fires on a specific action (e.g., form fill); auto re-enrolls each time trigger occurs |
| **Filter-based** | Complex segmentation criteria; re-enrollment requires leaving then re-meeting criteria |
| **Schedule-based** | Runs on a set schedule; auto re-enrolls at scheduled time, no separate re-enrollment option |

### Key building blocks
- **Actions**: Send internal email/in-app notification, Send email, **Set marketing contact status**, Delay, Branch
- **Delays**: calendar date, date property, event occurrence, set amount of time, day of week, time of day
- **Branches**: One property/action output, **AND/OR logic**, Random distribution by %
- **Goals**: mark contacts as "done" once a goal is met (e.g., list membership) — only for workflows sending marketing email; improves reporting clarity

### Enrollment & unenrollment management
- **Unenrollment tab** (in enrollment trigger panel): block/unenroll based on suppression list, goal met, or no-longer-meets-criteria
- **Merged contact enrollment status** — toggle on/off (e.g., off for external engagement to preserve consent)
- **Connections settings**: auto-unenroll from all/specific other workflows when enrolled in this one
- **Manually add contacts**: via enrollment triggers, custom filter, list, or individual contacts
- Workflow must be **turned on** (Review and publish → Turn on workflow) to run

### Analyzing performance
`Automations → Workflows → Analyze tab` — total enrollments, running workflows, % change
`Health tab` — similar/redundant workflows, workflows needing review, unused workflows

### Real-world examples (Blue Frog agency)
- **Bratney** — notifies sales reps of website visits from contacts they own (filtered to US traffic, branched by "last activity date" to avoid over-notifying)
- **Seconn Fabrication** — independent workflow that immediately sets bounced/unsubscribed contacts to non-marketing to protect the paid contact tier
- **Cascadia Daily News** — "abandoned cart" style nurture: form fill → branch on purchase completion → staggered delay/email series (1hr → 6hr → 24hr) → converted 20% of drop-offs to customers

#tags: #workflows #automation

---

## 9. Understanding Social Media

> [!abstract] Value of social in HubSpot
> Schedule/publish content, monitor feeds/competitors, connect to campaigns, and report on performance — all in one tool.

### Strategic benefits
1. Expand marketing reach
2. Build brand awareness
3. Drive word-of-mouth (Forbes: 71% of consumers with good social experience recommend the brand)
4. Attract buyers, tie into campaigns
5. Communicate directly → build trust/loyalty

> [!tip] Foundation first
> Define your **buyer persona** before building a social strategy (informs content mix and timing) — and connect social efforts to broader **marketing campaigns**.

### Connect points across marketing
- Social handles in email signatures/newsletter footers
- Social links in website header/footer
- Promote Facebook lead ads in social channels
- Auto-share blog posts to social

### Setup (`Settings → Marketing → Social`)
- **Connect accounts**: Facebook (incl. Instagram), X, LinkedIn, YouTube Reports
- Choose default accounts per post
- **Publish now by default** toggle; **Publish like a human** (varies exact time ±10 min window); **Next post delay** dropdown
- Optional Chrome extension + Bitly integration
- Auto-publish blog posts to a chosen social channel (`Choose blog`)
- Enterprise: grant draft-only permissions via Users & Teams

### Publishing tool
`Marketing → Social → Manage → Create social posts`
- Select accounts (e.g., Instagram + YouTube) → draft copy (can vary per platform) → add emoji/link (blog post or landing page) → **Generate with Copilot** (Breeze AI) for copy/hashtags
- Per-platform edits: Instagram Content Type (Post/Reel/Story), add media
- **Publish now** or **Schedule for later**; optionally link to a **marketing campaign**
- YouTube requires Title*, Description*, Video*, Audience* (plus optional Playlist/Tags/Language/License)

### Publishing schedule
`Settings → Marketing → Social → Publishing tab` → Add time per day/column → Apply → delete underperforming time slots via trash icon

### Calendar & management
`Marketing → Social → Calendar` — drag/drop to reschedule; **Clone** a post to reuse/edit (note: X blocks near-duplicate reposts)
**AI Agent → Calendar events → View Suggestions** — auto-suggested posts for holidays/awareness days; Regenerate Image/Copy & Hashtags; Schedule

### Reporting (`Marketing → Social → Analyze`)
| Report | Measures |
|---|---|
| Audience | Current followers (Facebook Page = *likes*, not followers) |
| Published Posts | # posts published (incl. outside HubSpot) |
| Interactions | Likes/reactions/comments (X retweets excluded here, counted in Shares) |
| Clicks | Only trackable for posts published **through HubSpot** (shortened links) |
| Shares | Includes X retweets; excludes LinkedIn personal profile & Instagram shares |
| Impressions | First-time unique views (FB/IG/LinkedIn Company Pages) |
| Sessions | Site sessions driven by social (any source, any time) |
| New Contacts | New contacts created from social-driven sessions |

Manage page also lets you filter by account/mode/date/campaign/user and see **Published from** (HubSpot vs. external).

#tags: #social-media #publishing #reporting

---

## 10. Creating a Campaign

> [!abstract] Definition
> A **marketing campaign** = "a connected series of operations designed to bring about a particular result" — a focused, single-goal effort (not all marketing activity).
> *Marketing campaign ≠ advertising campaign*: advertising (paid media) is just one component of a broader marketing campaign.

### Examples
- Nike product release (billboard + Instagram + email = one campaign)
- Apple **"Shot on iPhone"** — product-launch campaign, brand + user-generated content combined

### Planning checklist
1. **Goals & KPIs** — quantify + how measured (HubSpot/Google Analytics/Looker)
   - Email: CTR, Bounce rate, Conversion rate
   - Paid Social: CTR, Conversion rate, CPC, Cost/conversion
   - Organic Social: passive/active engagements, follows, CTR
   - Content Offers: opt-in rate, cost/opt-in, follow-up open rate
   - Display/Paid Media: CPM, CTR, conversion rate, cost/conversion
   - SEO: CTR, bounce rate, time on page, scroll depth, conversion rate
2. **Marketing channels** — which perform best / allow paid promo / best engagement?
3. **Budget** — agency, ads, freelance costs → feed into ROI analysis
4. **Content formats** — video, press releases, guest blogs, etc.
5. **Team** — in-house, agency, or freelance/contractor roles
6. **Design concept** — consistent with parent brand but own visual identity
7. **Deadlines** — start date + deadline drive promo cadence
8. **Analysis owner** — who measures success post-campaign

> [!tip] HubSpot pro-tips
> - Keep landing pages, forms, and CTAs **cohesive** to guide toward the goal
> - Use **marketing tasks** to stay organized
> - Use the **Marketing Calendar** to track content
> - Use **social/email scheduling** tools to reduce daily posting pressure

### Success definition
A campaign **"works"** if it meets its goal; it's **"worthwhile"** if ROI is proportionate to effort invested.

### Building a campaign
`Marketing → Campaigns (under Planning and Strategy) → Create campaign`
1. Name it (⚠️ **cannot be changed later**)
2. Description + approximate start date (+ budget, target personas, end date if time-sensitive)
3. **Edit goals** — target visits, contacts, customers
4. Associate assets in 3 sections:
   - **Convert Contacts** — landing pages + forms
   - **Promote Campaign** — emails, blog posts, site pages
   - **Nurture Contacts** — workflows

### Reporting on campaigns
Two ways:
1. **Campaign tool itself** — auto-populates visits, contact growth, emails sent, CTA clicks, etc.
2. **Reporting & Data → Reports → Analytics Tools → Campaign Analytics**

Five core metrics:
| Metric | Meaning |
|---|---|
| **Sessions** | Traffic to campaign-related assets |
| **New Contacts (first touch)** | New contacts first brought in by this campaign |
| **New Contacts (last touch)** | New contacts whose conversion is most attributed to this campaign |
| **Influenced Contacts** | All contacts (new+existing) who engaged with campaign assets |
| **Closed Deals** | Closed-won deals tied to influenced contacts |
| **Influenced Revenue** | Closed revenue from those deals |

Visualize by area/column/line; toggle campaigns for comparison; export as XLSX/XLS/CSV.

#tags: #campaigns #strategy #reporting

---

## 11. Understanding Reporting

> [!abstract] What marketing reporting does
> Gathers/analyzes metrics to inform decisions, strategy, and performance — reveals which channels work, gaps in strategy, and supports budget/headcount advocacy.

### 1️⃣ Traffic Reports
`Reporting & Data → Reports → Traffic` (under Report collections)
Key questions to answer:
- What trends/spikes/dips appear over time?
- Which sources drive the most traffic (organic, social, referral, direct)?
- Which pages/content over/underperform?
- Any geographic/demographic patterns to target?

### 2️⃣ Analyze Tabs (per-tool)
Every tool in the **Marketing** sidebar has an **Analyze** tab (e.g., Email → Analyze, Social → Analyze).
- **Exception**: Campaigns → open specific campaign → **Performance** tab
- **Compare feature**: campaign → Actions → **Compare campaign** (also available for email, social, forms, CTAs, SMS)

### 3️⃣ Custom Report Builder
`Reporting & Data → Reports → Create report → Custom Report Builder`
- Choose **primary data source** (e.g., Contacts) + optional secondary sources
- Drag properties to **X-axis**, **Y-axis**, and **Break down by**
- Example: Create Date (X) × Count of Contacts (Y) × Persona (breakdown) = contacts-by-persona-over-time report
- Add **Filters** tab for date range/property filters
- Save → name it (or **Generate** description via AI) → choose: don't add to dashboard / add to existing / add to new dashboard

> [!tip] Contacts-by-persona pro tips
> - Review **monthly** to catch persona imbalances and see campaign impact
> - Get comfortable with the report builder generally (know your X/Y/filter options) for future custom reports

### 4️⃣ Marketing Analytics Suite (Pro/Enterprise)
`Reporting → Marketing Analytics`
- **Quick answers** section (top) — prebuilt Q&A reports; "See all" for full list; fallback to **Chat with Chatspot** or Help Center
- Left sidebar → **Marketing → [topic]** (e.g., Channel performance → Forms, Ads, Email, SMS)
- **About this report** panel — explains metrics/usage
- **Filters tab** — date range, frequency, grouping/breakdown, compare vs. another date range
- Per-report metric toggles (e.g., Forms: Submissions / Views / Conversion rate) + **Edit columns**
- **Save report** → name/description → add to dashboard
- **Advanced reporting** (Enterprise) — customer journey analytics & attribution

### 5️⃣ Contact Create Attribution
`Reports → Create report → Attribution` → use a **prebuilt reporting question/template** (recommended for beginners) or **Create a custom report from scratch**
- Configure: **Chart type**, **Attribution model(s)** (multiple = shown separately), **Dimensions** (asset title/type, interaction source — add more via "Add another dimension")
- Common filters: **Contact create date** (week starts Sunday), **Asset types**, **Campaigns**
- Pinpoints which marketing activities created new contacts

> [!tip] Pro-tip
> Run contact create attribution reports **quarterly**. If a channel (e.g., Facebook) drives strong results, invest more there.

### 6️⃣ Customer Journey Reports (Enterprise)
`Reports → Create report → Customer Journey Reports` → select **Contacts** data source
- Drag **Steps** onto the **Timeline** (up to 5 steps/stage for parallel pathways)
- **Mark as optional** for non-essential stages (first & last stage cannot be optional)
- Uses **Sankey charts** (unique to this report) — visualizes flow/conversion between stages
- Click **Run report** → filter at top → view step-by-step conversion metrics in the table below the chart

> [!tip] Pro-tip
> Build a customer journey report for every major conversion path — even top offers often reveal room to optimize.

#tags: #reporting #analytics #attribution

---

## 🔗 Cross-topic connections
- **Personas** → inform **Segmentation** (lists) → drive **Email** & **Social** targeting
- **Forms** & **CTAs** → feed into **Campaigns** (Convert/Promote sections) → trigger **Workflows** (Nurture section)
- **Workflows** commonly reference **Lists** (List Membership trigger) and set **marketing contact status** for data hygiene
- **Reporting** (Analyze tabs, Custom Report Builder, Attribution, Campaign Analytics) ties every tool's performance back to the **Contacts Database**

## 📌 Key numbers to remember
- 74% of marketers use forms for lead gen; 49.7% call forms their top converter
- 77% of marketers saw email engagement boost; 99% check inbox daily
- Personalized CTAs perform **202% better** than generic ones
- Reducing form fields 11→4 improved conversion **120%** (Imagescape)
- Single-column forms complete **15.4 sec faster** (CXL Institute)
- 71% of consumers with good social experiences recommend the brand (Forbes)
