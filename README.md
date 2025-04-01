<div dir="rtl" style="text-align:right;direction:rtl;>

  # Easy-GPU-PV

## معرفی
یک پروژه در حال توسعه که با هدف ساده‌سازی مجازی‌سازی جزئی GPU در ویندوز Hyper-V طراحی شده است!

GPU-PV به شما امکان می‌دهد که GPU اختصاصی یا مجتمع سیستم خود را تقسیم کرده و آن را به چندین ماشین مجازی Hyper-V اختصاص دهید. این همان فناوری‌ای است که در WSL2 و Windows Sandbox استفاده می‌شود.

Easy-GPU-PV فرآیند راه‌اندازی یک ماشین مجازی GPU-PV را با خودکارسازی مراحل موردنیاز ساده‌تر می‌کند.

## قابلیت‌های Easy-GPU-PV
این ابزار موارد زیر را انجام می‌دهد:
1) ایجاد یک ماشین مجازی به انتخاب شما
2) نصب خودکار ویندوز روی ماشین مجازی
3) تقسیم‌بندی GPU انتخابی و کپی فایل‌های درایور موردنیاز به ماشین مجازی
4) نصب [Parsec](https://parsec.app) روی ماشین مجازی برای اتصال راه دور با تأخیر کم

## پیش‌نیازها
* **سیستم‌عامل:** ویندوز 10 نسخه 20H1+ (Pro، Enterprise یا Education) یا ویندوز 11 (Pro، Enterprise یا Education)؛ پیشنهاد می‌شود هم میزبان و هم ماشین مجازی از ویندوز 11 استفاده کنند.
* **نسخه‌های یکسان ویندوز** بین میزبان و ماشین مجازی برای جلوگیری از ناسازگاری.
* **کارت گرافیک:** کامپیوتر دسکتاپ با GPU اختصاصی NVIDIA/AMD یا GPU مجتمع Intel؛ لپ‌تاپ‌هایی با GPUهای NVIDIA در حال حاضر پشتیبانی نمی‌شوند.
* **درایورهای به‌روز:** دانلود آخرین نسخه درایور GPU از Intel.com یا NVIDIA.com.
* **فایل ISO ویندوز:** دریافت آخرین نسخه ویندوز 10 یا 11 از مایکروسافت (بدون استفاده از Media Creation Tool).
* **فعال‌سازی قابلیت مجازی‌سازی در BIOS** و [فعال‌سازی کامل Hyper-V](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) در ویندوز.
* **اجازه اجرای اسکریپت‌های PowerShell** با اجرای دستور زیر در PowerShell با دسترسی Administrator:
```powershell
Set-ExecutionPolicy unrestricted
```

## دستورالعمل‌ها
1. اطمینان حاصل کنید که سیستم شما پیش‌نیازهای لازم را دارد.
2. [مخزن را دانلود و استخراج کنید.](https://github.com/jamesstringerparsec/Easy-GPU-PV/archive/refs/heads/main.zip)
3. PowerShell ISE را با دسترسی Administrator اجرا کنید.
4. فایل `PreChecks.ps1` را در PowerShell ISE باز کرده و اجرا کنید.
5. فایل `CopyFilesToVM.ps1` را باز کرده و مقادیر موردنیاز (RAM، فضای ذخیره‌سازی، مسیر فایل ISO و نام GPU) را تنظیم کنید.
6. `CopyFilesToVM.ps1` را اجرا کنید (ممکن است 5 تا 10 دقیقه طول بکشد).
7. وارد Parsec در ماشین مجازی شوید و از آن برای اتصال استفاده کنید.
8. سیستم شما آماده استفاده است!

## ارتقای درایورهای GPU پس از به‌روزرسانی درایور GPU میزبان
پس از به‌روزرسانی درایورهای GPU میزبان، باید درایورهای GPU ماشین مجازی را نیز به‌روزرسانی کنید:
1. پس از به‌روزرسانی درایور GPU، میزبان را مجدداً راه‌اندازی کنید.
2. PowerShell را به عنوان Administrator اجرا کنید و به دایرکتوری حاوی `CopyFilesToVM.ps1` و `Update-VMGpuPartitionDriver.ps1` بروید.
3. دستور زیر را اجرا کنید:
```powershell
Update-VMGpuPartitionDriver.ps1 -VMName "نام ماشین مجازی شما" -GPUName "نام GPU شما"
```

## نکات مهم
- **از Parsec برای اتصال به ماشین مجازی استفاده کنید** و آداپتور ویدیوی Hyper-V را غیرفعال کنید.
- اگر با خطای `ERROR: Cannot bind argument to parameter 'Path' because it is null.` مواجه شدید، احتمالاً فایل ISO را با Media Creation Tool دانلود کرده‌اید که پشتیبانی نمی‌شود.
- یک نمایشگر متصل یا دانگل HDMI باید به GPU متصل باشد تا Parsec بتواند صفحه را ثبت کند.
- در صورت اجرای سریع سیستم، ممکن است قبل از نصب درایورهای Parsec به صفحه ورود برسید، اما این درایورها به‌زودی نصب خواهند شد.

## تشکر از:
- [Hyper-ConvertImage](https://github.com/tabs-not-spaces/Hyper-ConvertImage)
- [gawainXX](https://github.com/gawainXX) برای کمک در تست و رفع اشکالات

این یک راهنمای کامل برای راه‌اندازی GPU-PV با Easy-GPU-PV در ویندوز Hyper-V است. امیدوارم مفید باشد!
</div>
