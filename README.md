  # SW-Lab
Software Lab @ SUT
---
Contributors: Amirmahdi, Helia and Farhad
---

  
## پرسش‌ها
علاوه بر گزارش آزمایش، پاسخ سوالات زیر را هم داخل فایل README بنویسید:
1. پوشه‌ی .git چیست؟ چه اطلاعاتی در آن ذخیره می‌شود؟ با چه دستوری ساخته می‌شود؟
وقتی یک مخزن گیت ایجاد می‌شود، پوشه‌ای به نام .git به همراه آن ساخته می‌شود. این پوشه تمام اطلاعات مربوط به گیت را ذخیره می‌کند. با اجرای دستور git init، این پوشه ایجاد می‌شود و در طول پروژه، فایل‌های داخل آن تغییر می‌کنند یا فایل‌های جدیدی به آن اضافه می‌شوند. در زیر، بخش‌های مختلف این پوشه را توضیح می‌دهیم:

- دایرکتوری objects: در ابتدا تنها شامل پوشه‌های info و pack است، اما با پیشرفت پروژه، پوشه‌های دیگری نیز به آن اضافه می‌شود. تمامی فایل‌هایی که منتظر کامیت شدن هستند، در این پوشه قرار دارند. به طور کلی، این دایرکتوری به عنوان محل ذخیره‌سازی اطلاعات شناخته می‌شود.
- دایرکتوری refs: شامل دو زیرپوشه است: heads که همه شاخه‌ها را در بر می‌گیرد و tags که همه نشانه‌های تاریخچه را شامل می‌شود. در پوشه heads، فایلی به نام master وجود دارد که به آخرین کامیت اشاره دارد. با ایجاد یک شاخه جدید، فایلی با همان نام و اشاره به آخرین کامیت ساخته می‌شود. در پوشه tags، دو نوع نشانه وجود دارد: نشانه‌های ساده (lightweight tags) که مانند فایل‌های پوشه heads فقط به آخرین کامیت اشاره دارند و نشانه‌های توضیح‌دار (annotated tags) که شامل اطلاعاتی مانند نام، ایمیل، تاریخ و پیام tagging هستند.
- دایرکتوری info: اطلاعات بیشتری درباره مخزن گیت در این پوشه وجود دارد. یکی از فایل‌های مهم این پوشه، فایل exclude است که مشخص می‌کند کدام الگوها باید نادیده گرفته شوند. برای مشخص کردن فایل‌ها و پوشه‌های نادیده گرفته شده، از فایل .gitignore استفاده می‌شود.
- دایرکتوری hooks: شامل اسکریپت‌های پیش‌فرض گیت است که در شرایط خاصی اجرا می‌شوند. مثلاً وقتی فرایند کامیت کامل می‌شود.
- فایل HEAD: به شاخه فعال اشاره دارد و به گیت می‌گوید که کدام شاخه در حال حاضر استفاده می‌شود.
- فایل config: شامل تنظیمات پیکربندی مخزن است که می‌تواند به صورت کلی برای همه مخازن یا به صورت محلی برای یک مخزن خاص تعریف شود. تنظیماتی مانند نام، ایمیل و ویرایشگر در این فایل مشخص می‌شوند.
- فایل description: می‌توان توضیح کوتاهی درباره مخزن در این فایل نوشت، اما اگر از gitweb استفاده نمی‌کنید، این فایل کاربرد زیادی ندارد.

2. منظور از atomic بودن در atomic commit و atomic pull-request چیست؟ در سیستم کنترل نسخه، یک کامیت اتمیک به کامیتی اطلاق می‌شود که تمامی تغییرات آن به صورت همزمان و به عنوان یک واحد غیرقابل تقسیم در مخزن ثبت می‌شود. به این ترتیب، وضعیت دقیق کد در هر لحظه قابل مشاهده است و امکان بازگردانی تغییرات آن کامیت در صورت نیاز وجود دارد.
منظور از درخواست واکشی اتمیک نیز این است که هر درخواست واکشی (pull request) به صورت یک کامیت منفرد در تاریخچه پروژه ثبت شود و در صورت بروز مشکل، آن درخواست واکشی به صورت کامل بازگردانده شود
3. تفاوت دستورهای fetch و pull و merge و rebase و cherry-pick را بیان کنید. دستور fetch: این دستور شاخه‌های موجود در مخزن راه‌دور (remote repository) را در مسیر refs/remotes// به‌روزرسانی می‌کند. این عملیات امن است زیرا شاخه‌های محلی در مسیر refs/heads را تغییر نمی‌دهد.

دستور pull: این دستور شاخه‌های موجود در مخزن محلی را با نسخه‌های راه‌دور آنها به‌روزرسانی می‌کند و همچنین سایر شاخه‌های مخزن راه‌دور نیز به‌روزرسانی می‌شوند.

دستور merge: با استفاده از این دستور، تغییرات یک شاخه با شاخه دیگر ترکیب شده و یک کامیت ادغام جدید ایجاد می‌شود. این کار تاریخچه کامیت هر دو شاخه را حفظ می‌کند و می‌تواند بیش از یک کامیت والد داشته باشد. از این دستور زمانی استفاده می‌شود که حفظ یک تاریخچه مشخص از شاخه‌ها اهمیت دارد.

دستور rebase: این دستور عملکردی مشابه با merge دارد اما کل شاخه feature را به بالای شاخه main منتقل می‌کند. این کار باعث حفظ تاریخچه کامیت به صورت خطی می‌شود. به این ترتیب شاخه feature به‌روز می‌شود در حالی که شاخه main تغییر نمی‌کند. این دستور زمانی استفاده می‌شود که می‌خواهیم قبل از ادغام شاخه‌ها، تغییرات شاخه feature را با تغییرات اخیر شاخه main هماهنگ کنیم.

دستور cherry-pick: با این دستور می‌توان یک کامیت مشخص را از یک شاخه انتخاب کرده و در شاخه دیگر اعمال کرد. هر دو دستور rebase و cherry-pick کامیت‌های یک شاخه را بر روی شاخه دیگر قرار می‌دهند، با این تفاوت که در rebase، کامیت‌های شاخه فعلی به شاخه دیگر منتقل می‌شوند و در cherry-pick، کامیت‌های شاخه دیگر به شاخه فعلی کپی می‌شوند.
4. تفاوت دستورهای reset و revert و restore و switch و checkout را بیان کنید.  دستور reset: با استفاده از این دستور، می‌توان بین کامیت‌ها جابجا شد و به این ترتیب کامیت‌ها را از شاخه حذف یا اضافه کرد. انجام این عملیات همواره تاریخچه کامیت را تغییر می‌دهد.

دستور restore: با استفاده از این دستور، می‌توان فایل‌های داخل working tree را از طریق index یا یک کامیت دیگر بازیابی کرد. این دستور شاخه را تغییر نمی‌دهد و می‌تواند برای بازیابی فایل‌های داخل index یک کامیت دیگر استفاده شود.

دستور revert: با این دستور، یک کامیت جدید ایجاد می‌شود که تغییرات کامیت‌های دیگر را بازگردانی می‌کند.

دستور checkout: این دستور چندکاره است. اگر به صورت git checkout <file> استفاده شود، تغییرات فایل‌ها را بازگردانی می‌کند و هنگامی که می‌خواهیم تغییرات فایل‌ها را قبل از stage کردن لغو کنیم، به کار می‌رود. این دستور عملا همان کاربرد دستور git restore را دارد. اگر به صورت git checkout <branch> استفاده شود، می‌توان بین شاخه‌ها جابجا شد که مشابه دستور git switch عمل می‌کند.

دستور switch: این دستور عملا همان git checkout <branch> است که برای جابجایی بین شاخه‌ها استفاده می‌شود.
5. منظور از stage یا همان index چیست؟ دستور stash چه کاری را انجام می‌دهد؟ 
به ناحیه stage که بین workspace و مخزن (repository) قرار دارد، شاخص (index) می‌گویند. این شاخص تمامی تغییرات را قبل از انجام کامیت، جمع‌آوری می‌کند. زمانی که مشغول کار هستیم، تغییرات در workspace باقی می‌مانند و می‌توانیم با استفاده از دستور git add، آنها را به مرحله stage یا index منتقل کنیم. سپس با کامیت کردن، تغییرات موجود در index را در مخزن ثبت می‌کنیم.

دستور git stash زمانی استفاده می‌شود که بخواهیم تغییرات موجود در working directory فعلی را ذخیره کنیم تا بتوانیم به یک دایرکتوری دیگر برویم و بعداً به این تغییرات بازگردیم. این دستور تغییرات محلی را ذخیره کرده و working directory را به حالتی بازمی‌گرداند که با کامیت HEAD همخوانی دارد.

6. مفهوم snapshot به چه معناست؟ ارتباط آن با commit چیست؟ (راهنمایی: [لینک](https://github.blog/2020-12-17-commits-are-snapshots-not-diffs/)) snapshot از چیزی، به معنای ثبت حالت کنونی آن چیز در یک نقطه خاص از زمان است. کامیت‌ها به نوعی یک snapshot زمانی هستند زیرا شامل یک اشاره‌گر به root tree بوده و نشان‌دهنده حالت working directory در هر لحظه می‌باشند.
7. تفاوت‌های local repository و remote repository چیست؟
8.  مخزن محلی (local repository)، یک کپی از تاریخچه پروژه و codebase است که در سیستم توسعه دهنده قرار دارد. این مخزن به توسعه دهندگان امکان می‌دهد که به صورت آفلاین کار کنند، ایده‌های مختلف را آزمایش کنند، و workflow خصوصی خود را داشته باشند.

در مقابل، remote repository به عنوان یک هاب محلی عمل می‌کند که در آن توسعه‌دهندگان می‌توانند با یکدیگر همکاری کنند و کارشان را با دیگران به اشتراک بگذارند. این نوع مخزن یک پشتیبان برای پروژه فراهم می‌کند و این امکان را برای افراد تیم به وجود می‌آورد که تغییراتشان را با یکدیگر هماهنگ کنند.

تفاوت‌های local repository و remote repository به شرح زیر است:

امکان کار آفلاین در یک local repository فراهم است.
سرعت کار و انجام عملیات‌های گیت به صورت محلی سریعتر است.
توسعه‌دهندگان برای آزمون ویژگی‌های جدید، تغییر کد، و تست کردن رویکردهای متفاوت،آزادی عمل بیشتری برای کار به صورت local دارند.
در remote repository، همکاری آسان‌تر است زیرا مخزن remote به عنوان نقطه مرکزی synchronization عمل می‌کند و به افراد تیم اجازه می‌دهد که تغییرات‌شان را با یکدیگر merge کنند.
کار کردن با یک remote repository یک backup برای codebase ایجاد می‌کند.
در صورتی که دستگاه‌های محلی دچار آسیب شوند، کدهای موجود در remote repository آسیب نمی‌بینند بنابراین امنیت پروژه نیز تأمین می‌شود.

#

</div>
