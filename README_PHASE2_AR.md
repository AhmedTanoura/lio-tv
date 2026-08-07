# Lio TV — PHASE 2 / Laravel Foundation

هذه الحزمة هي **بداية المشروع الفعلية** وليست نسخة نهائية من Lio TV.

## ما تم تنفيذه في هذه المرحلة

- هيكل Laravel 12 متوافق مع PHP 8.2+.
- إعداد MySQL / MariaDB في `.env.example`.
- صفحة بداية Lio TV داكنة ومتجاوبة.
- Health route الافتراضي: `/up`.
- أمر Artisan: `php artisan lio:status`.
- فحص متطلبات السيرفر: `php tools/preflight.php`.
- جدول `users` الأساسي المتوافق مع تصميم Phase 1.
- جداول Laravel الأساسية للـ cache / jobs متاحة من خلال migrations.
- اختبارات Foundation للصفحة الرئيسية وHealth route.
- لا يوجد Login أو Owner Panel حتى الآن؛ هذا يبدأ في Phase 3 ثم Phase 4.

## لماذا لا يوجد مجلد vendor داخل ZIP؟

`vendor` يحتوي مكتبات Laravel التي ينزلها Composer. لا يتم حفظه كمصدر للمشروع. بعد فك الضغط شغّل `composer install` لتنزيل نسخ الحزم المطابقة لـ `composer.json` وإنشاء autoload.

## تشغيل محلي — خطوة بخطوة

1. ثبّت PHP 8.2 أو أحدث + Composer + MySQL/MariaDB.
2. افتح Terminal داخل مجلد المشروع.
3. شغّل:

```bash
php tools/preflight.php
composer install
```

4. أنشئ ملف البيئة:

Windows CMD:
```bat
copy .env.example .env
```

Linux / macOS:
```bash
cp .env.example .env
```

5. افتح `.env` واكتب بيانات قاعدة MySQL.
6. شغّل:

```bash
php artisan key:generate
php artisan migrate
php artisan lio:status
php artisan test
php artisan serve
```

7. افتح المتصفح على:

`http://127.0.0.1:8000`

ويجب أن ترى صفحة **LIO TV — PHASE 2 FOUNDATION**.

8. افتح:

`http://127.0.0.1:8000/up`

ويجب أن يعيد السيرفر حالة HTTP 200.

## ملاحظة cPanel

لا ترفع المشروع للإنتاج قبل التأكد من أن الاستضافة توفر Composer أو تسمح برفع مجلد `vendor` الذي تم إنشاؤه في بيئة PHP متوافقة. يجب توجيه Document Root للدومين/الساب دومين إلى مجلد `public`، أو استخدام ترتيب cPanel آمن يحقق نفس النتيجة. لا تجعل جذر Laravel نفسه متاحًا للعامة.

## إعدادات Shared Hosting الأولية

- `SESSION_DRIVER=file`
- `CACHE_STORE=file`
- `QUEUE_CONNECTION=sync`

هذه الإعدادات لا تحتاج Redis ولا Worker دائم. سنعدل الـ Queue عندما نبدأ مهام M3U والـ Scheduler.

## حدود Phase 2

لم يتم تنفيذ الميزات التالية عمدًا حتى الآن:

- Login / Logout
- Owner setup
- Roles & Permissions
- Resellers
- Points
- Content management
- M3U imports
- API v1
- Backups
- Reports

وجود ملفات أو أسماء مستقبلية لن يعني أن الميزة جاهزة؛ سننفذ كل مرحلة ثم نختبرها قبل الانتقال لما بعدها.
