
https://github.com/ambrop72/badvpn


https://www.youtube.com/watch?v=52lTdyu7i6c
https://gist.github.com/1nikolas/4efbfb6b0d37eba8c9ab471c55f5e892
```
sudo wget -O /usr/bin/badvpn-udpgw "https://raw.githubusercontent.com/daybreakersx/premscript/master/badvpn-udpgw64"
sudo touch /etc/rc.local
sudo nano /etc/rc.local

----------------------
#!/bin/sh -e
screen -AmdS badvpn badvpn-udpgw --listen-addr 127.0.0.1:7300
exit 0
----------------------

chmod +x /etc/rc.local
sudo systemctl status rc-local.service
sudo chmod +x /usr/bin/badvpn-udpgw
sudo screen -AmdS badvpn badvpn-udpgw --listen-addr 127.0.0.1:7300
reboot
sudo lsof -i -P -n | grep LISTEN







```


badvpn udpgw این چیه؟ و کی نوشتش آیا اوپن سورسه؟

###### ChatGPT said:

ChatGPT

**BadVPN udpgw** یک ابزار از پروژه‌ی **BadVPN** است که برای بهبود عملکرد VPNها و تونل‌ها استفاده می‌شود.

### **کاربرد udpgw:**

این ابزار به عنوان یک **UDP Gateway** عمل می‌کند و امکان انتقال ترافیک **UDP** از طریق یک تونل **TCP** (مانند VPN یا SSH Tunnel) را فراهم می‌کند. از آنجا که بیشتر تونل‌ها به طور پیش‌فرض فقط **TCP** را پشتیبانی می‌کنند، BadVPN udpgw این مشکل را حل کرده و امکان استفاده از برنامه‌هایی که نیاز به UDP دارند (مانند VoIP، بازی‌های آنلاین، و DNS) را در این تونل‌ها فراهم می‌کند.

### **چه کسی BadVPN را نوشته است؟**

BadVPN توسط **Ambroz Bizjak** ایجاد شده است. او این پروژه را برای استفاده در شبکه‌های خصوصی، تونلینگ، و برخی کاربردهای پیشرفته طراحی کرده است.

### **آیا BadVPN و udpgw اوپن سورس است؟**

بله، **BadVPN** و همه ابزارهای آن، از جمله **udpgw**، اوپن سورس هستند و تحت **GNU GPLv3 License** منتشر شده‌اند. کد منبع آن در GitHub در دسترس است، و هر کسی می‌تواند آن را دانلود کرده، تغییر دهد و استفاده کند.

### **چرا از آن استفاده کنیم؟**

1. **سبک و ساده:** طراحی شده برای اجرا در سیستم‌های سبک، مانند سرورهای کوچک یا حتی روترها.
2. **انعطاف‌پذیری:** می‌توان آن را با انواع تونل‌ها و VPNها ادغام کرد.
3. **قابلیت UDP:** مشکل عدم پشتیبانی تونل‌ها از UDP را رفع می‌کند.

### **چطور نصب و استفاده کنیم؟**

1. **نصب از منبع (Source):** کد را از [ریپوی GitHub](https://github.com/ambrop72/badvpn) دانلود کنید و با استفاده از کامپایلر **CMake**، آن را نصب کنید.
    
    bash
    
    Copy code
    
    `git clone https://github.com/ambrop72/badvpn.git cd badvpn mkdir build cd build cmake .. -DBUILD_NOTHING_BY_DEFAULT=1 -DBUILD_UDPGW=1 make`
    
2. **اجرای سرور udpgw:** دستور زیر را برای اجرای سرور **udpgw** بزنید:
    
    bash
    
    Copy code
    
    `./badvpn-udpgw --listen-addr 127.0.0.1:7300`
    
    این دستور سرور را روی پورت 7300 اجرا می‌کند.
    

### **چطور استفاده کنیم؟**

پس از اجرای udpgw، کلاینت (مثل نرم‌افزارهای تونلینگ) باید تنظیم شود تا ترافیک UDP خود را به این سرور هدایت کند.

اگر اطلاعات بیشتری نیاز داری یا مشکل خاصی پیش آمده، بگو تا کمک کنم! 😊