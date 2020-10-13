---
title: ساخت افزونه وردپرس - با rest api عاشق شوید
date: 1399-07-22 11:30:00
sitemap_date: 2020-10-13 11:30:00
author: Mohammad Javad Ghasemy
comments: true
rtl: true
picture: geeksesi-ir_make-wordpress-plugin-rest-api.jpeg
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

سلام، خب رسیدیم به مبحث شیرین گشادی با ای‌پی‌آی (Rest Api).

از اونجاییکه من خیلی بحث‌های مربوط به PWA, SPA رو دوست دارم از بک‌اندی که ای‌پی‌آی نداشته باشه خوشم نمیاد، فلذا همیشه سعی می کنم ای‌پی‌آی بسازم بعد اینور بیام با ریکت و داستان های دیگه هندلش کنم و یه فرانت خوب بزنم تنگش.

خب خیلی حرف نزنیم بریم سراغ بحثمون. اینبار خیلی ساده فقط می خواهیم یه سری مسیر بسازیم و آشنا بشیم با اینکه این مسیر ها توی وردپرس چجوری دارن کار می کنن.

# Wordpress Rest Api

خب کارمون اینجا هم با چنگ و دندون (Hook) پیش میره، منتها یکم تعداد قلابامون زیاد میشن نگران نباشید، سخت نگیرید و لذت ببرید.

```php
/**
 * Make Beautiful Rest Api
 */

add_action('rest_api_init', "LHWPP_rest_route_init");

function LHWPP_rest_route_init()
{
    register_rest_route('lhwpp/v1', 'hello', [
        "methods" => "POST",
        "callback" => "LHWPP_rest_hello_handler",
    ]);
}

/**
 * Route : site-url/wp-json/lhwpp/v1/hello
 * Method : POst
 * input : null
 * output : string
 *
 * @return string
 */
function LHWPP_rest_hello_handler()
{
    $output = [];
    $output["ok"] = true;
    $output["message"] = "Hello World I'm Panda";

    $out = json_encode($output);
    return $output;
}
```

خب این کد و لینک های زیر رو داشته باشید تا هرجایی که بتونم رو سعی می کنم توضیح بدم.

-   [rest_api_init Hook](https://developer.wordpress.org/reference/hooks/rest_api_init/)
-   [register_rest_route()](https://developer.wordpress.org/reference/functions/register_rest_route/)
-   [ چجوری ای‌پی‌آي وردپرس را گسترش دهیم به زبان سخت](https://developer.wordpress.org/rest-api/extending-the-rest-api/)

خب برای اینکه به وردپرس حالی کنیم یه مسیر ای‌پی‌آی بهمون بده باید یه قلاب بندازیم سمتش و مسیرمون رو توی تابعی که سر قلاب وصل می کنیم تعریف کنیم.

تابع `register_rest_route` برای ما مسیر می سازه. ورودی های تابع هم از این قراره :

## register_rest_route

-   namespace : اسمی که برای این گروه از مسیر های پلاگین انتخاب می‌کنیم ()

-   -   حواستون باشه که اینجا هم باید یه اسم کاملا شاخص انتخاب کنید
-   -   نکته بعد اینکه ورژن یادتون نره. ممکنه در آینده بخواهید تغییری توی مسیرهاتون ایجاد کنید و هنوز کلاینت هایی باشن که بروز نشدن. برای جلوگیری از درگیری اسم مسیر رو اینجوری تعیین کنید : `namespace/version`

-   route : اسم مسیر (چون اسم گروهی خاص انتخاب کردید دیگه نیاز نیست نگران درگیری اسم مسیرتون با ما بقی پلاگین ها باشید)
-   option : تنظیمات و یک سری مواردی که برای مسیر‌هاتون باید مشخص کنید
-   -   methods :‌ POST | GET | PUT | HEAD | DELETE | ... [More Information](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
-   -   callback : تابعی که می خواهیم به ریکوئست های ای‌پی‌آی مون رسیدگی کنیم.

## به همین راحتی تموم شد ؟

اره دیگه تموم شد، شاخ فیل که نمی‌خواستیم بشکنیم.

API تون با ادرس `SITE_URL.com/wp-json/namespace/route` در دسترسه. اگر هم نبود به تنظیمات پیوندیکتا وردپرستون مراجعه کنید.

به پایان آمد این دفتر (یادم رفت لینک‌های داخلی رو بزارم همین آخر پست می زارم. شما ندیده بگیر رد شو برو)

# اگر مطالب قبلی را هنوز نخوانده اید و یه سره اومدید سر وقت این مطلب :

-   [مخزن گیت‌هاب افزونه‌ای که داریم می سازیم](https://github.com/geeksesi/learn-how-to-make-wordpress-plugin)
-   [پست اول در مورد اینکه چجوری یه افزونه وردپرس رو شروع کنیم](https://geeksesi.ir/1399/07/18/make-wordpress-plugin-make-first-plugin/)
-   [پست دوم - صفحه ادمین و صفحه تنظیمات برای پلاگین خودمون بسازیم](https://geeksesi.ir/1399/07/19/make-wordpress-plugin-add-admin-panel/)
-   [پست سوم - با پلاگین وردپرس خود ابزارک بسازید](https://geeksesi.ir/1399/07/21/make-wordpress-plugin-how-create-custom-widget-by-plugin/)
