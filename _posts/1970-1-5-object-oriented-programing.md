---
layout: post
title: برنامه نویسی شی گرا
chapter: بخش دوم - فصل پنجم
author: علی رضائیان
---


همانطور که خواهیم دید اساس یک معماری نرم افزار خوب فهم و بکاربردن طراحی شی گرایی است.

شی گرایی چی هست؟
به عبارتی مدل کردن دنیای واقعی در نرم افزار توسط یک سری پارادایم که در ادامه گفته می شود.

  [Encapsulation](#encapsulation) 

  [Inheritance](#inheritance) 

  [Polymorphism](#polymorphism) 


ترکیب این سه پارادایم شی گرایی را شکل میدهد و هر زبان شی گرا میبایست این سه پارادایم را ساپورت کند.

## Encapsulation

 ایجاد سطح دسترسی برای یک دسته بهم پیوسته از function و data  که در  یک کلاس قرار میگیرند(فقط function ها از خارج کلاس قابل دسترسی (public) است و data قابل دسترسی نیست (private))

 مثال صفحه ۵۳ پیاده سازی encapsulation را در زبان C انجام داده است  که این اصل به طور کامل رعایت شده است و کلاس خارجی فقط امکان  فراخوانی function های کلاس header را دارد و هیچ اطلاعی از نحوه پیاده سازی و dataStructure آن ندارد.

در زبان C++ به دلیل این که کامپایلر نیاز داست تا به data فایل .h دسترسی داشته باشد پیاده سازی encapsulation مقداری تغییر کرد و از حالت ایده‌آل خارج شد و باعث شد که این اصل نقض شود.
درحالی کامپایلر سطح دسترسی به data کلاس header را محدود کرده بود اما بازهم نمیشد گفت که encapsulation  رعایت شده است به این دلیل که کلاس های client قادر بودند data کلاس header را مشاهده کنند.

با این حال روش پیاده سازی encapsulation با معرفی کلیدواژه های سطح دسترسی (public private protected) مقداری اطلاح شد.

> Java and C# simply abolished the header/implementation split altogether, 
>thereby
>weakening encapsulation even more. In these languages, it is impossible to 
>separate
>the declaration and definition of a class.

بر اساس دلایلی که ذکر شد oo وابستگی خاصی به encapsulation نداشت و اغلب زبان های oo هیچ اصراری هم بر پیاده سازی آن نداشتند.

با این حال میبایست برنامه نویس ها افراد معتمدی باشند تا encapsulation را  دور نزنند.
( زبان هایی که ادعا می کنند oo را ارائه میکنند, encapsulation یی که ما از آن به طور کامل در  زبان C لذت میبردیم  الان به شکل ضعیف شده بکار میبرند)

## Inheritance

به زبان ساده inheritance دوباره تعریف کردن دسته ای از متغییرها و فانکشن ها که در یک محدوده خاص هستند است.

در مثال صفحه ۵۶ در فانکشن main مشاهده میشود که NamedPoint از Point مشتق گرفته شده است و اعضای Point را داخل خودش نگهداری میکند

این مثال مربوط به قبل از این که oo ابداع شود نوشته شده است و همانطور که مشاهده میشود‌ازیک روش مرسوم برای inheritance استفاده کرده است (pointer =*)

 (در زبانهایی مثل C &#x202b; inheritance به شکل cast کردن explicit بود اما در زبان های oo این نوع cast کردن به شکل  implicit انجام می شود) 

با توجه به این که قبلان از این روش استفاده میشد اما این روش مناسبی نیست و حتی برای حالت هایی مثل multiple inheritance کار سخت میشود.

## Polymorphism

همچون بقیه پارادایم های oo که قبلان ذکر شد polymorphism هم قبل oo وجود داشته است.

در مثال اولی که آورده شده است عملکرد function بسته به نوع STDIN و STDOUT تغییر میکند.
سوالی که طرح شده است با فراخوانی متد getchar چگونه کاراکترهای دریافت شده درایور دستگاه خوانده میشود؟
هر سیستم unix نیاز به درایورهای دستگاه های I/O داردکه آنها  ۵ فانکشن را ارئه میدهند
(open , close, read , write , seek)   این فانکشن ها برای همه درایور ها دارای signiture یکسانی هستند.
درایور io برای consule (مثل interface در سایر زبانها) اینها را تعریف خواهد کرد
(مطابق شکل صفحه۳۸۶)
این consule میتواند به شکل های مختلفی (در اینجا STDIN) پیاده سازی شود.
در C++ هر virtualFuncton داخل کلاسی قرار داده شده است که دارای یک pointer در جدولی است که vtable نامیده میشود.
و فراخوانی همه virtualFunction ها از طریق جدول انجام میشود.
کلاس های مشتق شده به سادگی این function ها را با ورژن های خودشان در ابجکتی که از vtable ساخته شده است load میکنند.
درنهایت polymorphism  را میتوان به عنوان یک اپلیکیشن pointer به functionها نام برد.
از زمان معماری Von Neumann در اواخر ۱۹۴۰ برنامه نویس ها از pointer ها برای پیاده سازی polymorphism استفاده میکردند.
اما آن به طور کامل صحیح نیست. زبان هایOO ممکن است نتوانند polymorphism را به طور کامل ارائه کنند بدلیل این که آن میبایست امن تر و همچنین استفاده از آن راحتتر باشد.
مشکل استفاده از pointer ها در عملکرد polymorphism خطرناک بودن pointer ها در function ها است
برنامه نویس مجبور هست که همیشه مقداردهی pointerها و فراخوانی function ها را درذهن داشته باشد در غیر این صورت سیستم دچار مشکل میشود و بررسی مشکل بسیار سخت میشد

زبان های oo این قواعد را حذف کنند تا استفاده از polymorphism به براحتی قابل انجام باشد.
براین اساس تصمیم گرفته شد که در OO قاعده جابه‌جایی غیرمستقیم کنترل اعمال شود.

~~~~
قدرت polymorphisms چه هست؟
مثال copy برنامه را درنظر بگیرید.
اگر یک دستگاه جدید io ساخته شود در آن برنامه چه اتفاقی می‌افتد؟
در واقع هیچ اتفاقی نمی‌افتد. پیاده سازی متدها درخود دستگاه ها انجام شده است. و سیستم فقط function را فراخوانی میکند. به عبارت دیگر سیستم هیچ وابستگی به دستگاه ندارد(سورس کد درایور)
~~~~


>OO allows the plugin architecture to be used anywhere, for anything.


## Dependency Inversion


![](assets/di.png)

در شکل 5.1 نوع پیاده سازی ایده‌ال polymorphism را نشان داده است
نکته ای که برای main در این شکل وجود دارد جایی که HL فراخوانی میشود به اعلان اسم ماژول به طور explicit نیاز است.
این مدل dependency در مسیرجریان پروژه به شکلی است که به طبع آن عملکرد سیستم هم تحت تاثیر قرار میگیرد.
 در شکل 5.2  ماژول HL1 فانکشن f را که در ماژول ML1 قرار دارد از طریق یک interface فراخوانی میکند.(در زمان اجرای برنامه interface  وجود ندارد و HL1 فانکشن داخل ماژول ML1 را فراخوانی میکند)
درحالی که مسیر جریان  وابستگی سورس کد بین ML1 و interface به شکل مخالف است.
حقیقت ارائه امن و راحت polymorphism در زبان های oo این است که 'وابستگی سورس کد مهم نیست که در کجا است, میتواند معکوس شود' 
با این شیوه معماران نرم افزار در زبان های oo بر مسیرجریان وابستگی های سیستم کنترل مطلق دارند. (This is the power)

وقتی که این قدرت بکار برده می شود چه اتفاقی می افتد؟
شما میتوانید وابستگی های سورس کد در سیستم را بطوری دوباره بچینید که UI و DB به BusinessRule وابسته باشند (شکل 5.3)
این به این معنی است که UI و DB میتوانند به BusinessRule به عنوان پلاگین وصل شوند. به عبارت دیگر سورس کد BusinessRule هیچ گاه به UI و DB وابسته نیست.
و به همین ترتیب این ماژول ها قادر هستند به طور مستقل در سه کامپوننت مجزا یا واحدهای deployment کامپایل شوند.
واحد BusinessRule به بدون هیچ وابستگی قابل deploy شدن است و به همین ترتیب تغییرات واحدهای UI یا  DB هیچ اثری بر سیستم ندارد 



> In short, when the source code in a component changes, only that 
>component needs
>to be redeployed. This is independent deployability.
>If the modules in your system can be deployed independently, then they can >be developed independently by different teams. That’s independent 
>developability.

## Conclution

oo چیست؟
برای این جواب نظرات مختلفی وجود دارد. برای معماری نرم افزار جواب کاملان مشخص است
oo یک توانایی است. که سه پارادایم درون خودش دارد.
به طور مثال به واسته polymophism امکانی که به معمار نرم افزار میدهد این است که میتواند بر مسیرجریان سیستم کنترل داشته باشد, این به معمار نرم افزار مکان ساخت ماژول هایی با قابلیت plugin شدن را میدهد, که در آن ماژولها قواعد سطح بالایی وجود دارد که به طور کامل مستقل از ماژول هایی است که دارای جزییات سطح پایین است. 

