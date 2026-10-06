# تطبيق المحاضرات التعليمية — مدرسة الإخلاص (أندرويد / Kotlin)

تطبيق أندرويد أصلي (Kotlin + Jetpack Compose + Material 3).
الشاشات: **ترحيب ← قائمة المحاضرات ← مشاهدة الفيديو داخل التطبيق**.
لا حسابات ولا قاعدة بيانات ولا سيرفر. الإنترنت مطلوب فقط لتشغيل الفيديو.

---

## أسهل طريقة للحصول على APK (بدون تثبيت أي برنامج)

1. أنشئ حسابًا مجانيًا على **github.com**.
2. **New repository** ← اختر **Private** ← أنشئه.
3. اضغط **uploading an existing file** وارفع **كل** محتويات هذا المجلد (بما فيها المجلد المخفي `.github`) ثم **Commit**. (اسم الفرع `main`)
4. تبويب **Actions** ← **Build Android APK** ← **Run workflow**.
5. بعد 4 إلى 7 دقائق تظهر علامة ✓ خضراء. افتح التشغيل ونزّل **alekhlas-apk** ← فك الضغط ← `app-release.apk`.
6. أرسله للطلاب. على الهاتف: افتح الملف ← اسمح بـ «التثبيت من مصادر غير معروفة» ← تثبيت.

## أو: البناء على جهازك بـ Android Studio

1. حمّل وثبّت **Android Studio** من developer.android.com/studio
2. **File ← Open** واختر هذا المجلد، وانتظر انتهاء المزامنة (Sync) — قد يطلب تنزيل أدوات، اضغط Accept/OK.
3. للتجربة: وصّل هاتفك (تفعيل USB debugging) واضغط ▶ Run.
4. لبناء APK: **Build ← Build Bundle(s) / APK(s) ← Build APK(s)** ثم اضغط **locate**.
   الملف في: `app/build/outputs/apk/release/app-release.apk` (اختر نوع البناء release).

---

## إضافة محاضرة جديدة

افتح الملف الوحيد: `app/src/main/java/com/alekhlas/lectures/Lectures.kt` وأضف سطرًا:

```kotlin
val lectures = listOf(
    Lecture("محاضرة قوانين السير", "rMVZwpDlARo"),
    Lecture("محاضرة الميكانيكا", "sKbqPG386-c"),
    Lecture("محاضرة الإشارات", "P_EMWF63d_o"),
    Lecture("عنوان المحاضرة الجديدة", "معرّف_الفيديو"),   // ← جديد
)
```
`معرّف_الفيديو` هو الجزء بعد `youtu.be/` في الرابط (11 حرفًا).
بعد التعديل أعد بناء الـ APK وأرسله للطلاب.

## تعديل النصوص

`app/src/main/res/values/strings.xml` — كل نصوص التطبيق في هذا الملف.

## تغيير ألوان الهوية

`app/src/main/java/com/alekhlas/lectures/ui/Theme.kt` — الكائن `Brand` في الأعلى:
```kotlin
val Blue   = Color(0xFF0B2BE0)
val Orange = Color(0xFFFF6A00)
val Red    = Color(0xFFE31B1B)
```

## استبدال الشعار

- شعار الشاشات: استبدل `app/src/main/res/drawable/logo.jpg` بشعارك **بنفس الاسم**.
- أيقونة التطبيق على الهاتف: في Android Studio اضغط يمين على `res` ← **New ← Image Asset** واختر شعارك.

---

## ملاحظات

- الفيديو يعمل عبر **YouTube IFrame Player API الرسمي** داخل التطبيق بأدوات التحكم الرسمية دون تعديل عليها. لذلك قد يظهر شعار YouTube وعنوان الفيديو داخل المشغّل، وهذا من سياسات YouTube.
- أي رابط داخل المشغّل يحاول فتح موقع آخر يتم حظره، فلا يخرج الطالب من التطبيق.
- يجب أن يكون **التضمين مسموحًا** لكل فيديو: YouTube Studio ← تفاصيل الفيديو ← «السماح بالتضمين».
- الـ APK موقّع بمفتاح debug، يصلح للتوزيع المباشر. للنشر على Google Play تحتاج مفتاح توقيع خاصًا.
- بدون إنترنت تظهر رسالة: «يحتاج تشغيل المحاضرة إلى اتصال بالإنترنت.»
