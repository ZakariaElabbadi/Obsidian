ماذا سنفعل بالضبط؟

سنقسم Slack إلى 3 مستويات:

المستوى 1 — ربط Salesforce ↔ Slack

أول شيء سنفهم:

Salesforce Org
     ↕
Salesforce for Slack
     ↕
Slack Workspace
     ↕
Channels / Users

في Salesforce توجد إعدادات Salesforce for Slack / Slack Apps Setup، ومن هناك يتم تفعيل التكامل والصلاحيات. Salesforce توضح أن إعداد التكامل يتطلب تفعيل Slack integrations ثم إعطاء المستخدمين الصلاحيات المناسبة.

وبما أنك تستخدم Developer Edition، فهذا مهم جدًا: التكامل الأساسي مع Slack متاح في Developer Edition.

المستوى 2 — Slack داخل Flow Builder ⭐

وهذا هو الجزء الذي أريد أن نركز عليه معًا.

بعد الربط، عندما تعمل:

Flow → Action

ستجد Category اسمها:

Slack

ومن خلالها توجد Actions مثل:

Send Slack Message
Create Slack Channel
Add Users to a Slack Channel
Archive Slack Channel
Edit Slack Message
Get Information about Slack Conversation
Check if Users Are Connected to Slack
وغيرها.

يعني بدل:

Opportunity Closed Won
        ↓
Send Email
        ↓
Customer receives Email

سنستطيع عمل:

Opportunity Closed Won
        ↓
Send Slack Message
        ↓
#sales
        ↓
🎉 Opportunity Closed Won!

وهذا بالضبط النوع الذي أريدك أن تتعلمه.

المستوى 3 — Flow يعمل من داخل Slack 🔥

وهنا تصبح الأمور أجمل.

ليس فقط:

Salesforce → Slack

بل أيضًا:

Slack → Salesforce Flow

مثلاً موظف في Slack يضغط زر:

Create Follow-up Task

فتشغل العملية:

Slack
  ↓
Button
  ↓
Screen Flow
  ↓
Create Task
  ↓
Salesforce

Salesforce تدعم حاليًا Screen Flows يمكن جعلها Available in Slack، ويمكن تشغيلها من Slack.

بل يوجد Action اسمه:

Send Message to Launch Flow

بحيث يرسل Flow رسالة إلى Slack تحتوي على زر، والموظف يضغط الزر لتشغيل Screen Flow.

مثال عملي سنبنيه لاحقًا

أريد أن نصل إلى شيء مثل هذا:

Opportunity
     │
     │ Stage = Closed Won
     ↓
Record-Triggered Flow
     │
     ├──────────────→ Email Alert
     │
     └──────────────→ Slack
                         │
                         ↓
                  #sales-channel
                         │
                         ↓
              🎉 New Deal Won!
              
              Opportunity: CRM Project
              Amount: $50,000
              Owner: Zakaria

وهنا ستتعلم فعليًا كيف تجمع:

Flow + Salesforce Data + Email + Slack

وما الذي تحتاج أن تعرفه في Slack؟

ليس مطلوبًا أن تصبح Slack expert 😄.

بالنسبة لمسارك في Salesforce، سنركز على:

1. Workspace

المكان الذي توجد فيه الشركة.

2. Channels

مثلاً:

#sales
#marketing
#support
#general
3. Users / Members

من يستقبل الرسالة.

4. Slack App

التطبيق الذي يسمح لـSalesforce بالتعامل مع Slack.

5. Salesforce ↔ Slack Connection

عملية الربط والمصادقة.

6. Slack Permissions

من يستطيع الاتصال واستخدام التكامل.

7. Slack Flow Actions

وهي أهم شيء بالنسبة لك.

8. Slack Messages

كيف نرسل:

Text
Variables
Salesforce fields
Formatting
Links

مثلاً:

🎉 Opportunity Closed Won!

Opportunity: {!$Record.Name}
Amount: {!$Record.Amount}
Owner: {!$Record.Owner.Name}

Salesforce تدعم أيضًا Slack formatting داخل Text Template عند استخدام التكامل الأصلي، مع ضرورة استخدام Plain Text بدل Rich Text لهذا الغرض.

وهناك شيء مهم جدًا بالنسبة لطريقتنا في الدراسة

لن نترك Flow ونبدأ كورس Slack كامل.

لا.

سنفعل:

Salesforce Flow
      +
     Slack

يعني كل مفهوم Slack نتعلمه سيكون له Flow عملي.

مثلاً:

Lesson	Flow
Connect Slack	ربط Org بالـWorkspace
Send Slack Message	Opportunity Closed Won → Slack
Slack Variables	إرسال Amount/Owner/Name
Channels	إرسال الرسالة إلى #sales
Users	إضافة مستخدم إلى Channel
Create Channel	إنشاء Channel من Flow
Screen Flow in Slack	تشغيل Flow من Slack
Button → Flow	Slack Button → Salesforce
Advanced	Slack + Decision + Get Records + Loop

وهكذا لن تكون معرفتك نظرية.

إذن عندما نبدأ بعد 3–4 ساعات، أقترح هذا الترتيب:

① نربط Slack بالـDeveloper Org

② نتأكد أن Slack يظهر داخل Flow Builder

③ أول Flow:

Opportunity Closed Won
        ↓
Send Slack Message

④ نضيف Salesforce Merge Fields

⑤ نرسل إلى Channel

⑥ نبني Flow أكثر احترافية باستخدام Decision / Get Records

⑦ بعدها نتعلم Slack → Salesforce

⑧ وأخيرًا Screen Flow داخل Slack

وهذا سيكون امتدادًا طبيعيًا جدًا لكل ما تعلمته حتى الآن في Flow، وليس موضوعًا منفصلًا.

والأهم: لا تحذف أو تغير شيئًا في الـOrg الآن 😂. عندما نبدأ، نمشي خانة بخانة، بيت بيت، دار دار، زنقة زنقة كما تعودنا. 😄

استرح الآن، وبعدها نبدأ من الربط نفسه وليس من Flow مباشرة.