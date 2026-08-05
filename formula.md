الفصل الذي سأخصصه لـ Formula

بعد أن ننتهي من Variables مباشرة.

الجزء 1 — أساسيات Formula
ما هي Formula؟
الفرق بينها وبين Variable
الفرق بينها وبين Assignment
متى أستخدم Formula؟
الجزء 2 — العمليات الحسابية
+
-
*
/
()
الجزء 3 — الدوال

مثل:

IF()

CASE()

AND()

OR()

NOT()

ISPICKVAL()

ISBLANK()

TEXT()

VALUE()

ROUND()

ABS()

MIN()

MAX()
الجزء 4 — التعامل مع النصوص
LEFT()

RIGHT()

MID()

LEN()

FIND()

SUBSTITUTE()

UPPER()

LOWER()

TRIM()
الجزء 5 — التاريخ
TODAY()

NOW()

YEAR()

MONTH()

DAY()

DATE()

DATEVALUE()
الجزء 6 — دمج النصوص

مثلاً:

Hello
Zakaria

↓

Hello Zakaria

أو

Welcome {!$Record.Name}
الجزء 7 — Picklist

ستتعلم لماذا نستخدم:

ISPICKVAL()

وليس:

=
الجزء 8 — أمثلة حقيقية

مثلاً:

إذا كان Amount أكبر من 10000

VIP Customer

وإلا

Regular Customer

أو

إنشاء Subject تلقائي:

New Opportunity - {!$Record.Name}
الجزء 9 — Formula متقدمة

مثل:

IF(
AND(),
OR(),
TEXT(),
ISPICKVAL()
)

في Formula واحدة.

بعدها ستكون قد أتقنت الموارد (Resources) الأساسية في Flow:
✅ Variable
✅ Constant
✅ Formula
✅ Text Template
✅ Choice (إذا احتجناها مع Screen Flows)
✅ Record Variable
✅ Record Collection Variable

وبعدها سندخل إلى Email، وسترى كيف نستخدم Formula + Variables + Text Templates معًا لإنشاء رسائل احترافية.

الخطة الحالية أصبحت بهذا الترتيب:

✅ Loops (انتهى)
⏳ Variables (ننهي ما تبقى)
⏳ Formula Resources (من الصفر إلى الاحتراف)
⏳ Text Templates
⏳ Email في Salesforce Flow (من الأساسيات إلى HTML وCSS وPDF)
⏳ بناء Flows احترافية تجمع كل ما تعلمناه

أعتقد أن هذا الترتيب سيجعلك تبني فهمًا متينًا بدلًا من تعلم الأدوات بشكل متفرق.

