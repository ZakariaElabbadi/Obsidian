الفصل الأول: أساسيات إرسال البريد في Flow
ما هو Send Email Action؟
ما هو Email Alert؟
ما الفرق بينهما؟
متى أستخدم كل واحد؟
الفصل الثاني: Send Email Action
إرسال إلى Email ثابت
إرسال إلى Email من Contact
إرسال إلى عدة أشخاص
CC
BCC
Reply-To
Sender Type
Subject
Body
الفصل الثالث: Email Alert
إنشاء Email Alert
ربطه بـ Flow
استخدام Email Template
Dynamic Recipients
الفصل الرابع: Email Templates
Text Template
HTML Email Template
Lightning Email Template
Classic Email Template

متى أستخدم كل واحد؟

الفصل الخامس: HTML داخل البريد

سنكتب بأنفسنا:

<h1>Welcome</h1>

<p>Hello {!Contact.FirstName}</p>

<table>...</table>

<img>

<a>

Buttons

Lists

Responsive Layout

وستتعلم كيف تضع متغيرات Salesforce داخل HTML.

الفصل السادس: CSS داخل البريد

ليس كل CSS يعمل داخل البريد.

سنتعلم:

Inline CSS
الألوان
الخطوط
Borders
Padding
Margin
Background
Rounded Buttons
Cards

وسأريك أيضًا ما الذي لا تدعمه Gmail وOutlook.

الفصل السابع: البريد الاحترافي

سنبني رسائل مثل:

Welcome Email
Thank You Email
Password Reset
Order Confirmation
Opportunity Closed Won
Case Escalated
Invoice Email
CRM Notification
الفصل الثامن: المرفقات
هل يمكن إرفاق PDF؟
هل يمكن إرسال Files؟
ContentVersion
Files
Attachments
Documents

وسنوضح القيود الموجودة في Salesforce Flow، ومتى نحتاج Apex أو أدوات أخرى.

الفصل التاسع: PDF

هنا سندرس:

Visualforce PDF
Flow + PDF
Screen Flow PDF
Quote PDF
Invoice PDF
إرسال PDF في البريد
الفصل العاشر: الاحتراف

سنبني مشاريع مثل:

عندما تصبح Opportunity = Closed Won
إنشاء PDF
إرساله للعميل
إرسال نسخة إلى المدير
تسجيل Email في النشاطات (Activities)
بعد إنهاء هذا الفصل ستكون قادرًا على إنشاء رسائل مثل:
──────────────────────────────
🎉 Welcome Zakaria

Thank you for choosing us.

---

Account:
Acme Corporation

Owner:
John Smith

Opportunity:
Enterprise License

Amount:
$25,000

---

Download your invoice

[Download PDF]

---

Best Regards
Sales Team
──────────────────────────────

مع أزرار، ألوان، تنسيق HTML، وربما PDF مرفق حسب السيناريو.

أرى أن أفضل وقت لبدء هذا الفصل هو بعد أن ننهي Variables بالكامل، لأن إرسال البريد يعتمد كثيرًا على المتغيرات، Record Variables، وText Templates. عندها سيكون من السهل عليك فهم كل الأمثلة وبناء رسائل احترافية بدل الاكتفاء بإرسال بريد بسيط



🎯 وبعد Formula

سندخل إلى فصل كنت متحمسًا له منذ البداية:

📧 Emails in Salesforce Flow

وسنجعله احترافيًا جدًا، يشمل:

Send Email Action
Email Alert
Email Templates
HTML
CSS
PDF
Dynamic Content
Attachments
أفضل الممارسات

وسيكون أقرب إلى دورة مستقلة.

# 📧 Salesforce Flow – Email Automation Roadmap

## أهداف الدرس

- ✅ الفرق بين **Send Email** و **Email Alert**
- ✅ كيفية إرسال Email من داخل Formula - Quick ReferenceFlow
- ✅ استخدام **Email Templates**
- ✅ استخدام **HTML** داخل البريد الإلكتروني
- ✅ استخدام **Rich Text**
- ✅ إدراج القيم الديناميكية (**Merge Fields**)
- ✅ إرسال **PDF كمرفق (Attachment)** ومتى يكون ذلك ممكنًا
- ✅ أفضل الممارسات لتجنب إرسال رسائل البريد المكررة
- ✅ مشروع عملي كامل:
  - عند إغلاق **Opportunity**
  - إرسال بريد إلكتروني احترافي للعميل
  - إنشاء **Task**
  - تحديث السجل (**Update Record**)