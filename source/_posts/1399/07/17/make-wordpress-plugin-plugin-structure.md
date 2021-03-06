---
title: ساخت افزونه وردپرس - ساختار افزونه
date: 1399-07-17 13:00:00
sitemap_date: 2020-10-08 13:00:00
author: Mohammad Javad Ghasemy
comments: true
rtl: true
picture:
tags:
    - وردپرس
    - افزونه وردپرس
    - php
    - wordpress
categories:
    - [اموزش, وردپرس]
    - [php, wordpress]
---

سلام. سعی می کنم با زبون بی زبونی توی 7 تا پست توضیح بدم که چجوری میشه یه افزونه وردپرس ساخت.

یه بخشی از کارمون مربوط میشه به اینکه چجوری کد افزونه های مختلف رو ببینیم. برای خوندن و کد افزونه‌ها نیاز داریم که اول بفهمیم ساختار یه افزونه چجوریه تا با دیدن فایل های زیاد و توابع عجیب و غریب شکه نشیم.

وظیفه‌ی دیگه ای که به عهده‌مونه اینه که بتونیم از دایکیومنت وردپرس استفاده کنیم. علمکرد و کار توابع و ساختار های عجیب غریبش رو یاد بگیریم تا بتونیم چیزی که می خواهیم رو بسازیم.

آخر کار هم شاید یه سری بزنیم به مسائلی که کمتر کسی ازشون سر در میاره. کارایی بکنیم که هیچ لزومی ندارن ولی ما از انجامشون لذت می بریم (یه حس خود شاخ پنداری داره).

## دقیقا با وردپرس چیکار داریم ؟

خب ما ۳ تا کار می تونیم با وردپرس انجام بدیم.

-   توسعه خود وردپرس
-   ساخت افزونه
-   ساخت قالب

اگه دوست دارید توی پروژه‌های نرم افزار آزاد شرکت کنید. یاد بگیرید. خودتون رو محک بزنید. با ساختار ها و ابزار هایی کار کنید که توی پروژه‌های کوچیک کمتر شانس این رو دارید که باهاشون آشنا بشید، بهترین انتخاب برای شما اینه که برید مخزن اصلی وردپرس رو فورک کنید و خودتون رو چالش بکشید تا بتونید یه چیزی به وردپرس اضافه کنید یا مشکلی رو ازش حل کنید.

البته خب فراموش نکنید که چیزی رو تغییر بدید که همه جامعه کاربری ازتون می خواد (به ایششو های گیت هاب مراجعه کنید)

اما اگه برنامه نویسی رو تازه شروع کردید. یا اصلا دنبال این هستید که به سایت خودتون چیزی رو اضافه کنید وقتشه از معجزه‌ای به اسم برنامه‌نویسی ماژولار استفاده کنید.

وردپرس به خاطر ساختار قلاب (hook) محوری که براتون فراهم کرده بهتون این اجازه رو میده تا افزونه‌هایی بنویسید که ماهیت وبلاگ بودن وردپرس رو زیر سوال ببره.

شما می تونید بدون حتی یک خط تغییر کد توی ساختار اصلی وردپرس و تنها با ساخت افزونه کل ساختار و ماهیت یه سایت وردپرس رو عوض کند. (نگران نباشید کار سختی نیست)

## ساختار وردپرس

قبل از اینکه بخواهیم شروع کنیم افزونه مون رو بسازیم باید بفهمیم قاطی این پوشه های وردپرس چی هست. ما اصلا با کدومش کار داریم.

وقتی اولین بار وردپرس رو نصب می کنید تغریبا با چنین منظره‌ای رو‌به‌رو می شید.

```
- wp-admin/
- wp-content/
    - plugins/
    - themes/
- wp-include/
- config.php
```

چیزی که برای ساخت افزونه بهش نیاز داریم توی مسیر `wp-content/plugins` وجود داره. اینجا می تونید دست به خلق چیز‌هایی بزنید که بقیه رو متحیر کنه.

تمام افزونه های وردپرس یه پوشه یا یه فایل php هستند توی این مسیر.

حالا که قاطی این فایل مایل ها هستید ساده ترین افزونه‌ای که با وردپرس ساخته شده رو همینجا نقدا نشونتون بدم.

برید به مسیر `wp-content/plugins/` یه فایل به اسم `hello.php` می بینید. این یه افزونست که اگه فعالش کنید اون بالا توی داشبورد براتون یه تیکه رندوم از متن آهنگ [hello dolley](https://www.metrolyrics.com/dolly-lyrics-the-refreshments.html) رو می زاره.

خب فکر کنم تا همینجا بس باشه. پست بعدی میریم سراغ اینکه اولین افزونه‌مون رو بسازیم.
