
## ✅ مرحله ۱: ساخت کلید SSH روی سیستم شما

```
ssh-keygen -t ed25519 -C "reza@your-email.com"
ssh-keygen -t rsa -b 4096 -C "reza@your-email.com"

# by default is ed25519
ssh-keygen -C "reza@your-email.com"

# if don't set -C name is : username@pcname
ssh-keygen 

```

## ✅ مرحله ۲: ارسال کلید عمومی به سرور

```
# میشه فقط همین رو اجرا کرد خودش میسازه پوش میکنه!
ssh-copy-id us


 ssh-copy-id -i /home/reza/.ssh/usserver us  
```


## نکته
اگه بخایم پاک کنیم فایل کی هارو ولی بازم تو رم سیستم میمونه با دستور زیر میشه پاک کرد.

```
# پاک کردن از رم
ssh-add -D 

# فینگرپرینت کوتاه|
ssh-add -l

# کلید عمومی کامل
ssh-add -L
```