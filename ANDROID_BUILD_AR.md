# الزهراء — تجهيز تطبيق Android

هذا الدليل يشرح تجهيز نسخة Android من مشروع الويب باستخدام Capacitor مع الاحتفاظ باتصال Supabase الحالي.

## المتطلبات
- Node.js 22 أو إصدار متوافق مع المشروع
- Android Studio حديث
- Android SDK وBuild Tools
- اتصال إنترنت لتنزيل حزم npm وGradle

## 1. إعداد Supabase
أنشئ ملف `.env.local` اعتمادًا على `.env.example` وأضف قيم مشروع Supabase الفعلية:

```env
VITE_SUPABASE_URL=https://YOUR_PROJECT.supabase.co
VITE_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_KEY
```

استخدم مفتاح anon/publishable المخصص للعميل فقط. لا تضع `service_role` أو أي سر داخل تطبيق الهاتف.

## 2. تثبيت الحزم وتجهيز Android
من جذر المشروع نفّذ:

```bash
npm install
npm run build
npm run android:add
npm run android:sync
npm run android:open
```

إذا كان مجلد `android` موجودًا بالفعل، تخطَّ `npm run android:add` ونفّذ المزامنة فقط.

## 3. إنشاء APK
في Android Studio انتظر اكتمال Gradle Sync، ثم اختر:
**Build > Build Bundle(s) / APK(s) > Build APK(s)**

ملف الاختبار عادةً:
`android/app/build/outputs/apk/debug/app-debug.apk`

لإنشاء نسخة توزيع، استخدم **Build > Generate Signed Bundle / APK** واحتفظ بمفتاح التوقيع بأمان.

## ملاحظات قبل النشر
- يلزم تثبيت حزم Capacitor وإضافة منصة Android قبل أن يتوفر مشروع Android الأصلي.
- يجب اختبار تسجيل الدخول، واستعادة الجلسة، ومزامنة البيانات، والفواتير والطباعة، ومشاركة الملفات على جهاز فعلي.
- مسارات الذكاء الاصطناعي النسبية مثل `/api/ai/status` و`/api/ai/simsim` تحتاج إلى API منشور عبر HTTPS أو إعداد عنوان API مناسب.
- تحقق من سياسات RLS في Supabase. لا تضمّن مفاتيح إدارية أو أسرارًا داخل APK.
