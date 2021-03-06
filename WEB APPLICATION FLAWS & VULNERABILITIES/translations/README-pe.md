
# Buffer Overflow

سرریز بافر یا یک بافر بیش از حد ، یک اشتباه رمزگذاری نرم افزار است که یک مهاجم می تواند از آن برای دستیابی به سیستم شما سوء استفاده کند. برای کاهش موثر آسیب پذیری های سرریز بافر ، مهم است که بدانید سرریزهای بافر چه هستند ، چه خطری برای برنامه های شما ایجاد می کنند و مهاجمان از چه تکنیکی برای سوء استفاده موفقیت آمیز از این آسیب پذیری ها استفاده می کنند.

- این خطا هنگامی رخ می دهد که داده های بیشتری در بافر وجود داشته باشد تا بتواند آن را کنترل کند و باعث سرریز اطلاعات در فضای مجاور شود.
این آسیب پذیری می تواند باعث خرابی سیستم شود یا بدتر از آن ، یک نقطه ورود برای حمله سایبری ایجاد کند - .

- C و C ++ مستعد ابتلا به سرریز بافر هستند.

- روشهای توسعه ایمن باید شامل آزمایش منظم برای تشخیص و رفع سرریزهای بافر باشد. این شیوه ها شامل حفاظت خودکار در سطح زبان و بررسی - محدودیت ها در زمان اجرا است.

### تعریف سرریز بافر

یک بافر بخشی از حافظه پی در پی است که شامل هر چیزی از یک رشته کاراکتر تا مجموعه ای از اعداد صحیح است. سرریز بافر یا غلبه بر بافر هنگامی اتفاق می افتد که داده های بیشتری در مقایسه با بافر سیستم با طول ثابت آن قرار گیرند. اطلاعات اضافی ، که باید به جایی بروند ، می توانند به فضای حافظه مجاور سرریز شوند ، داده های نگهداری شده در آن فضا را خراب یا ویرایش کنند. این سرریز معمولاً منجر به خرابی سیستم می شود ، اما همچنین فرصتی را برای مهاجمین ایجاد می کند که کد دلخواه خود را اجرا کند یا خطاهای کد نویسی را برای انجام اقدامات مخرب دستکاری کند.

بسیاری از زبانهای برنامه نویسی مستعد حملات سرریز بافر هستند. با این حال ، میزان چنین حملات بسته به زبان مورد استفاده برای نوشتن برنامه آسیب پذیر متفاوت است. به عنوان مثال ، کدی که در پرل و جاوا اسکریپت نوشته شده است معمولاً مستعد سرریز بافر نیست.

با این حال ، سرریز بافر در یک برنامه نوشته شده در
C ، C ++ ، Fortran یا Assembly
می تواند به مهاجم اجازه دهد تا سیستم هدفمند را به خطر بیاندازد.

مجرمان سایبری از مشکلات سرریز بافر برای تغییر مسیر اجرای برنامه با نوشتن قسمت هایی از حافظه آن سوء استفاده می کنند. اطلاعات اضافی مخرب ممکن است حاوی کدی باشد که برای تحریک اقدامات خاص ایجاد شده باشد - در واقع ارسال دستورالعمل های جدید به برنامه حمله شده که منجر به دسترسی غیرمجاز به سیستم می شود. تکنیک های هکر که از آسیب پذیری سرریز بافر بهره می برند ، در معماری و سیستم عامل متفاوت است.

خطاهای کدگذاری به طور معمول علت سرریز بافر هستند. خطاهای توسعه نرم افزارهای رایج که می تواند به سرریز بافر منجر شود شامل عدم 
اختصاص به اندازه کافی بافر و غفلت برای بررسی مشکلات سرریز است.

این اشتباهات به ویژه با 
C / C ++ مشکل دارند که محافظت داخلی در برابر سرریزهای بافر ندارند. در نتیجه ،برنامه های C / C ++ 
اغلب اهداف حملات سرریز بافر هستند

### نمونه حمله سرریز بافر

در برخی موارد ، یک مهاجم کدی مخرب را به حافظه تزریق می کند که در جریان سرریز خراب شده است. در موارد دیگر ، مهاجم به سادگی از سرریز و فساد آن در حافظه مجاور استفاده می کند. به عنوان مثال ، برنامه ای را در نظر بگیرید که از کاربر رمز عبور درخواست می کند تا کاربر بتواند به سیستم دسترسی داشته باشد. در کد زیر رمز عبور صحیح به امتیازات ریشه کاربر اعطا می شود. اگر گذرواژه نادرست باشد ، این برنامه امتیازات کاربران را اعطا نمی کند.

```c
printf ("\n Correct Password \n");
pass = 1;
}
if(pass)
{
/* Now Give root or admin rights to user*/
printf ("\n Root privileges given to the user \n");
}
return 0;
```
با این وجود احتمال سرریز بافر در این برنامه وجود دارد زیرا تابع
get () مرزهای آرایه را بررسی نمی کند.

در اینجا مثالی از آنچه مهاجم می تواند با این خطای کد نویسی انجام دهد ، آورده شده است:

```bash
$ ./bfrovrflw
Enter the password :
hhhhhhhhhhhhhhhhhhhh
Wrong Password
Root privileges given to the user
```

در مثال بالا ، این برنامه به کاربر امتیازات ریشه می دهد ، حتی اگر کاربر رمز عبور نادرستی را وارد کرده باشد. در این حالت ، مهاجمی ورودی با طول بیشتر از بافر را نگه می دارد و سرریز بافر را ایجاد می کند ، که حافظه عدد صحیح را پشت سر می گذارد. بنابراین ، با وجود گذرواژه نادرست ، ارزش "پاس" غیر صفر شد و مهاجم امتیازات اصلی دریافت می کند.

برای جلوگیری از سرریز بافر ، توسعه دهندگان برنامه های کاربردی C / C ++ باید از عملکردهای کتابخانه ای استاندارد که دارای مرز نیستند ، مانند بررسی ، اسکن و strcpy جلوگیری کنند.

بعلاوه ، روشهای توسعه ایمن باید شامل آزمایش منظم برای تشخیص و رفع سرریزهای بافر باشد. مطمئن ترین روش برای جلوگیری یا جلوگیری از سرریز بافر ، استفاده از محافظت خودکار در سطح زبان است. راه حل دیگر ، بررسی محدودیت ها است که در زمان اجرا اعمال می شود ، که با چک کردن خودکار اینکه داده های نوشته شده برای بافر در مرزهای قابل قبولی است ، از جلوگیری از بافر جلوگیری می کند.
