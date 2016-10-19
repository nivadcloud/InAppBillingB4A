
نمونه‌ای از استفاده از کتابخانه‌ی پرداخت نیواد 
----------------------------------------------

کتابخانه‌ی پرداخت نیواد راه حلی بی دردسر، حرفه‌ای و امن برای اضافه کردن پرداخت درون‌برنامه‌ای به اپلیکیشن‌های اندروید است.
این اپلیکیشن از کتابخانه‌ی پرداخت نیواد برای پیاده سازی پرداخت درون برنامه‌ای استفاده می‌کند.

**کتابخانه‌ی پرداخت نیواد با اتصال به سرورهای نیواد و بررسی وضعیت واقعی خرید اپلیکیشن و بازی شما را از جعل و هک پرداخت درون برنامه‌ای حفظ می‌کند**

شروع سریع!
----------

فایل‌های کتابخانه را دانلود کنید و در پوشهٔ

Libraries

بیسیک قرار دهید. به طور مثال اگر بیسیک را در درایو 

D

ویندوز نصب کرده باشید این پوشه در این آدرس قرار دارد:

    D:\Program Files (x86)\Anywhere Software\Basic4android\Libraries

در پنجرهٔ 

Libraries

بیسیک فور اندروید تیک مربوط به کتابخانهٔ نیواد را بزنید تا این کتابخانه به پروژه‌تان افزوده شود. اگر کتابخانهٔ نیواد در لیست موجود نبود، روی لیست راست کلیک کنید و گزینهٔ 

Reload

را انتخاب کنید.
در بخش 

Globals

اکتیویتی خرید این متغیر را تعریف کنید:

    Dim mNivadBilling As BillingProcessor
    
کدهای زیر را به متد 

Activity_Create

اضافه کنید:


    If FirstTime Then
        Dim bazaarRSAKey As String
        Dim nivadApplicationID As String
        Dim nivadBillingSecret As String
		
        bazaarRSAKey = "کلید RSA که از کافه بازار دریافت کردید"
        nivadApplicationID = "مقدار Application ID که در پنل نیواد، بخش پرداخت امن دریافت کردید"
        nivadBillingSecret = "مقدار Application Secret که در پنل نیواد، بخش پرداخت امن دریافت کردید"
		
        mNivadBilling.initialize(bazaarRSAKey, nivadApplicationID, nivadBillingSecret)
    End If

در منوی 

Tools

گزینهٔ 

Manifest Editor

را انتخاب کنید و خط زیر را به  آن اضافه کنید و فایل را ذخیره کنید:

    AddApplicationText(<activity android:name="io.nivad.billing.b4a.PurchaseActivity" />)

سابروتین‌های مربوط به پرداخت را اضافه کنید:


    Sub nivadbilling_purchase_history_restored()
       ' این متد زمانی صدا زده می‌شود که محصولاتی که کاربر خریده اما هنوز مصرف نشده‌اند از بازار دریافت شده اند. این محصولات را با متد‌های 
       ' isPurchased و isSubscribed 
       ' می‌توانید چک کنید
    End Sub

    Sub nivadbilling_product_purchased(sku As String, details As TransactionDetails)
       ' این روتین پس از خرید موفق صدا زده می‌شود
       ' برای محصولات مصرف شدنی اینجا تابع
       ' consumePurchase یا consumePurchaseInBackground
       ' را صدا بزنید و در صورتی که مقدار بازگشتی
       ' True
       ' بود اثر آن‌ را اعمال کنید.
    End Sub

    Sub	nivadbilling_initialized()
       'این روتین زمانی که سرویس پرداخت درون برنامه‌ای آماده‌ی کار می‌شود صدا زده می‌شود
       ' دکم‌های خرید را تا قبل از فراخوانی این متد فعال نکنید در غیر این صورت ممکن است برنامهٔ شما
       ' با خطا مواجه شده و بسته شود
    End Sub

    Sub nivadbilling_error(errorCode As Int)
	     ' این روتین در زمانی که اشکالی در فرایند پرداخت یا راه اندازی سرویس پرداخت درون‌برنامه‌ای به وجود بیاید صدا زده می‌شود.
       ' برخی از مقادیر پارامتر 
       ' code
       ' در آدرس زیر معرفی و توضیح داده شده اند:
       ' https://nivad.io/docs/iab-methods-and-error-codes/
    End Sub


تبریک! از الان برنامه‌ی شما می‌تواند پرداخت درون برنامه‌ای داشته باشد! پرداخت درون برنامه‌ای به صورتی که نه تنها راه‌اندازی‌ و استفاده از آن سریع‌تر و راحت‌تر از روش‌های دیگر است بلکه در مقابل ابزارهای جعل و هک پرداخت نیز ایمن و مقاوم است!

برای خرید یک محصول تابع 

purchase

را صدا بزنید:

    mNivadBilling.purchase("gold_version")
    
در مثال بالا، عبارت 

gold_version

شناسهٔ محصول در بازار است.
