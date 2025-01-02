
# udp is open or not!
```bash

// -u udp test 
// -z Only scan for listening daemons, without sending any data to them.

nc -zv -u 127.0.0.1 1080 



```



# Curl

```bash

 curl --proxy socks5://127.0.0.1:1080 http://icanhazip.com
```



# UDP traffic tracker

```bash
sudo tcpdump -i any udp port 1888
```



### بررسی و تست:

۱. **پینگ UDP:** از یک ابزار مثل `iperf` برای تست UDP از طریق SOCKS5 استفاده کنید.

```bash
iperf -c <server_ip> -u -p 1080
```

۲. **تست با ابزار خاص:** مثل `curl` یا کلاینت‌های خاص SOCKS که از UDP پشتیبانی می‌کنند.

> [!NOTE]
> من تست کردم packet ICMP ارسال میکرد!

