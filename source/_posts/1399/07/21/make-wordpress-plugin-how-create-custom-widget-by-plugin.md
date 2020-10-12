---
title: ساخت افزونه وردپرس - چطوری ابزارک (widget) بسازیم ؟
date: 1399-07-21 10:00:00
author: Mohammad Javad Ghasemy
comments: true
rtl: true
picture: geeksesi-ir_make-wordpress-plugin_how-create-widget.png
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

سلام.دفعات قبل عکس نمی زاشتم برای پست ولی خب به خاطر اینکه توی شبکه های اجتماعی پست خوشگل می‌شه با عکس ایندفعه رفتم یه چیزی پیدا کردم بزارم اون بالا، خیلی بهش دقت نکنید الکیه :))

# نگاهی کنیم به مطالب قبلی

خب قبل از اینکه شروع کنم به توضیح دادن یه سری لینک با توضیحات لیست می کنم این پایین دیگه بنابه نیاز خودتون استفاده کنید.

-   [مخزن گیت‌هاب افزونه‌ای که داریم می سازیم](https://github.com/geeksesi/learn-how-to-make-wordpress-plugin)
-   [پست اول در مورد اینکه چجوری یه افزونه وردپرس رو شروع کنیم](https://geeksesi.ir/1399/07/18/make-wordpress-plugin-make-first-plugin/)
-   [پست دوم - صفحه ادمین و صفحه تنظیمات برای پلاگین خودمون بسازیم](https://geeksesi.ir/1399/07/19/make-wordpress-plugin-add-admin-panel/)

صداش رو هم در نیارید که این لینک‌هایی که گزاشتم همش برای ایمپرشن جمع کردن و لینک داخلی گرفتنه :)))))

# قضیه چیه ؟

ببینید مطالبی که دارم می نویسم برای الان فقط توی فاز آشنایی شما با ابزارها و قابلیت‌هایی که توی افزونتون می تونید پیاده کنید.

با بحث پنل ادمین شروع کردیم، الان می خواهیم ویجت بسازیم، سراغ Rest Api میریم (از مباحث مورد علاقه منه) بعد دیگه دیوونه بازیمون قراره گل کنه و بزنیم بریم سراغ اینکه یه چیزی بسازیم و صد در صد این وسط با چیزهایی آشناتون می کنم که دیدتون رو نسبت به وردپرس یکمی تغییر بده.

# ابزارک بسازیم

خب این بار یکم اوضاع فرق می کنه. برای سایت و مدیریت یک ابزارک توی پلاگینمون باید یک کلاس بسازیم و از ساختار چنگ و دندون وردپرس می‌آییم بیرون.

قبل از اینکه شروع کنم یه سری لینک به دایکیومنت خود وردپرس می زارم (ماهی گیری یاد بگیرید.. برای انجام پروژه‌ها و یا ابزار‌هایی که می خواهید بسازید همیشه مطلب به این شکل فارسی و آماده پیدا نمیشه و باید برید دایکیومنت مرجع رو بخونید و متوجه بشید.)

-   [Wordpress widget Api](https://codex.wordpress.org/Widgets_API)
-   [WP_Widget class documantion](https://developer.wordpress.org/reference/classes/wp_widget/)

برای ساخت ابزارک باید اول یه کلاس بسازیم که از کلاس `WP_Widget` ارث و میراث می‌بره.

خب من کلاسم رو توی یه فایل دیگه توی پروژم به اسم `LHTMWPP_Widget.php` می زارم. (از اینکه اسم های عجیب غریب انتخاب می کنم شوکه نشید. به خاطر ساختار وردپرس برای اینکه اسامی کلاس ها و متد ها با هم قاطی نشن مجبوریم اینجوری اسم گزاری کنیم. این اسمی هم که می زارم مخفف اسم پلاگین هست)

فایل جدیدی که ساختم توی این مرحله چیزی شبیه اینه.

```
<?php

class LHTMWPP_Widget extends WP_Widget
{
}

```

خب الان باید هویت ابزارکمون رو تعریف کنیم. متد سازنده کلاسمون رو اینجوری من تعریف می کنم.

```
    public function __construct()
    {
        $my_widget = [
            'classname' => 'LHTMWPP_Widget',
            'description' => 'by this widget you will practice how to make widget',
        ];
        parent::__construct(
            'LHTMWPP_Widget',
            'Learn How To Make Wordpress Plugin - Widget',
            $my_widget
        );
    }
```

خب یه سری توابعی هستن این وسط که ما می تونیم بازنویسیشون کنیم ولی خب من فعلا فقط با یکیشون کار دارم، بقیه رو توی یه فرصت دیگه ازشون استفاده می‌کنیم.

تابع `widget` رو من به این شکل بازنویسی می کنم توی کلاسم :

```
    public function widget($args, $instance)
    {
        echo "HELLO it's my Widget";
    }
```

خب حالا باید از این کلاسی که برای ابزارک نوشتیم استفاده کنیم. بر می گردیم به فایل اصلی افزونمون.

قبلش یه نگاهی به ساختار پروژمون کنیم الان پوشه پروژه ما باید چنین حالتی داشته باشه :

```
- learn-how-to-make-wordpress-plugin :
    - learn-how-to-make-wordpress-plugin.php
    - LHTMWPP_Widget.php
```

خب حالا من چند خط به فایل `learn-how-to-make-wordpress-plugin.php` اضافه می کنم.

```
/**
 * Add Widget
 */

include 'LHTMWPP_Widget.php';

add_action('widgets_init', function () {
    register_widget('LHTMWPP_Widget');
});

```

خب باز هم یک قلاب جدید اطلاعات بیشتر در موردش رو می تونی از لینکی که می زارم بدست بیارید.

-   [widgets_init](https://developer.wordpress.org/reference/hooks/widgets_init/)

خروجی کارمون هم به این شکل شد.

![Theme > widgets > ShowCase](geeksesi-ir_make-wordpress-plugin_how-create-widget_show-case1.png)

![main website ShowCase](geeksesi-ir_make-wordpress-plugin_how-create-widget_show-case2.png)

خب برای امروز کارمون تمومه. شاد و خندون باشید.
