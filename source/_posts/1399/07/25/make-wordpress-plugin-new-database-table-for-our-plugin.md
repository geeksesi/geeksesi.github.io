---
title: ساخت افزونه وردپرس - برای افزونه خود جدول، دیتابیس بسازید
date: 1399-07-25 10:20:00
sitemap_date: 2020-10-16 10:20:00
author: Mohammad Javad Ghasemy
comments: true
rtl: true
picture:
tags:
    - وردپرس
    - افزونه وردپرس
    - php
    - wordpress
    - داشبورد ادمین
categories:
    - [اموزش, وردپرس]
    - [php, wordpress]
---

خب دیگه کم‌کم داره تعهد 7 تا پست آموزش وردپرس من تموم میشه. توی این ۲ تا آخری می خوام اگه بتونم سنگ تموم بزارم.

خب سریع بحث رو جدی کنیم که پروژه دارم خیلی وقت نوشتن ندارم.

# دیتابیس در وردپرس

خب اینبار می خوام چندتا مسئله رو بهم بپیچونم. قصد دارم توی این پست نشونتون بدم چجوری برای پلاگینتون یه جدول وردپرس ایجاد کنید و تابع ازش توی پلاگینتون استفاده کنید.

اولین مسئله ای که با ساخت جدول توی مای‌اسکیول مواجه میشیم قضیه مهاجرت (migration) هست که توی وردپرس خیلی کم بهش بها داده شده و برنامه‌نویس باید با دستای ناتوان خودش قضیه رو حل و فصل کنه.

منطق اینجوری کار می کنه. ما می خوایم بگیم هر وقت یه نفر پلاگین مارو فعال کرد برو و یه جدول دیتابیس برامون بساز.

خب حالا دوباره بریم تو کار چنگ و دندون اینبار یکم فرض داره قلابی که باید بندازیم نشونتون میدم.

-   [register-activation_hook](https://developer.wordpress.org/reference/functions/register_activation_hook/)

باید از این گل‌پسر (شاید بگید توابع مگه جنسیت دارن. اره ما می تونیم بهشون میدیم.) استفاده کنیم.

این شکلی :‌

```
register_activation_hook(__FILE__, 'LHWPP_plugin_activate');
function LHWPP_plugin_activate()
{
}

```

خب حالا باید اینجا یه مشته کد بریزیم که جدول مورد نظرمون رو توی دیتابیس وردپرس بسازه.

من یه جدول این شکلی تعریف می کنم (سعی می کنم از دیتا تایپ های مهم استفاده کنم که جنبه آموزشی داشته باشه )

خب من تابع رو اینجوری تغییر میدم بعد شروع می کنم به توضیح دادن

```
function LHWPP_plugin_activate()
{
    global $wpdb;
    $table_name = $wpdb->prefix . 'LHWPP_table';

    $sql =
        " CREATE TABLE " .
        $table_name .
        " (
        id                  BIGINT(20)   NOT NULL AUTO_INCREMENT,
        title               TEXT         NOT NULL,
        start_time          DATETIME     NOT NULL,
        finish_time         DATETIME         NULL,
        status              VARCHAR(20)  NOT NULL,
        PRIMARY KEY  (id)
    )" .
        $wpdb->get_charset_collate() .
        ";";

    require_once ABSPATH . 'wp-admin/includes/upgrade.php';
    dbDelta($sql);
    add_option('jal_db_version', '1.0.0');
    if ($wpdb->get_var("SHOW TABLES LIKE '" . $table_name . "'") != $table_name) {
        error_log("unable to make db");
        return false;
    }
    return true;
}
```

این رو از یکی از پروژه های قدیمیم برداشتم. یکم تغییرش دادم. الان کاملا جدول نامربوطیه :))

خب برای کارکردن با دیتابیس توی وردپرس ما همیشه نیاز به `$wpdb` داریم. خب مثل بچه آدم میاییم گلوبالش می‌کنیم که توی تابع دسترسی بهش رو داشته باشیم.

مسئله بعدی اسم جدول هست. از اونجاییکه موقع نصب وردپرس، پیشوند برای جداولمون تعریف می‌کنیم، توی افزونه هامون هم باید شروع اسم جداول با این پیشوند شروع بشه. که خب خیلی راحت با `$wpdb->prefix` مقدارش رو می گیریم.

حالا باید کوئری دیتابیس بزنیم که دیگه این قسمت رو توضیح نمی دم... برید آموزش mysql پیدا کنید و ببینید.

خب حالا برای اینکه بتونیم کوئری مون رو اجرا کنیم باید از تابع `dbDelta()` استفاده کنیم.

ولی خب در حالت عادی این تابع در دسترس نیست. باید از فایلش بگیریمش. پس قبل میریم که چرک بازی رو شروع کنیم (از نظر من وارد کردن یه فایل وسط یه مشت کد واقعا چرک بازیه ولی خب چیکار کنیم ؟ مجبوریم :))) )

خب شرح وظایف و کارکرد این `dbDelta` هم طولانیه لینک دایکیومنت می زارم.

-   [dbDelta](https://developer.wordpress.org/reference/functions/dbdelta/)

خب خط بعدی یه کار اختیاریه ولی عمل زیبا و پسندیده ایه.

خود وردپرس اینجوری در موردش توضیح داده :

```
Another excellent idea is to add an option to record a version number for your database table structure, so you can use that information later if you need to update the table:
```

ولی خب به من چه من که حوصله کار های زیبا و پسندیده رو ندارم. پس کامنتش می کنم بره.

خب حالا چک کنیم ببینیم جدولمون ساخته شده یا نه.

اگه نشده بود که سرور رو به خاک سیاه می‌نشونیم. اگر هم شده بود که از خبط و خطاش چشم پوشی کرده و اوکی بهش میدیم بره پی کارش.

# تموم شد -ـ-

خب قبل از اینکه تموم کنم این بخش رو حتما سوال می پرسید حالا که جدول رو ساختیم چجوری باهاش کار کنیم.

اشکال نداره بپرسید منم ارجاعتون میدم به دایکیومنت وردپرس. یه سری لینک می زارم که به دردتون می خوره.

-   [wpdb](https://developer.wordpress.org/reference/classes/wpdb/)
-   [creating table with plugin](https://codex.wordpress.org/Creating_Tables_with_Plugins)

# بیشتر بخوانید

بیایید یه مشته لینک می زارم اینجا و میرم

-   [افزونه وردپرس بسازیم !!؟](https://github.com/geeksesi/learn-how-to-make-wordpress-plugin)
-   [چگونه اولین افزونه وردپرس خود را بسازیم](https://geeksesi.ir/1399/07/18/make-wordpress-plugin-make-first-plugin/)
-   [برای افزونه وردپرس خود صفحه ادمین و صفحه تنظیمات بسازید](https://geeksesi.ir/1399/07/19/make-wordpress-plugin-add-admin-panel/)
-   [با پلاگین وردپرس خود ابزارک بسازید](https://geeksesi.ir/1399/07/21/make-wordpress-plugin-how-create-custom-widget-by-plugin/)
-   [وردپرس و گشادی با rest api](https://geeksesi.ir/1399/07/22/make-wordpress-plugin-fall-in-love-with-rest-api/)
