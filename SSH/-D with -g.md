
```bash
ssh -D 1080 -R 1080:localhost:1080 -g root@107.175.73.102
```

ssh -D 1122 -R 1080:localhost:1080 root@107.175.73.102 فک کنم این جا یک سویچ باید بزنیم که این ۱۱۲۲ رو عمومی کنه 0.0.0.0

###### ChatGPT said:

ChatGPT

بله، درست متوجه شدی! برای اینکه پراکسی SOCKS روی `0.0.0.0` (که یعنی همه آدرس‌های IP قابل دسترسی باشند) در کامپیوتر ۱ (PC1) در دسترس باشد، باید از سویچ `-g` استفاده کنی.

دستور اصلاح‌شده به این صورت می‌شود:

bash

Copy code

`ssh -D 1122 -R 1080:localhost:1080 -g root@107.175.73.102`

سویچ `-g` باعث می‌شود که پراکسی SOCKS که روی پورت ۱۱۲۲ راه‌اندازی می‌شود، به تمام IP‌ها (نه فقط `localhost`) قابل دسترسی باشد.

حالا PC2 می‌تواند از پراکسی SOCKS روی `192.168.1.227:1122` برای دسترسی به سایت‌ها استفاده کند.

4o mini
