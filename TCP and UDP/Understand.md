
> [!NOTE] چرا قطع میشه؟
> دلیل این رفتار اینه که `nc` به طور پیش‌فرض پس از دریافت یک بسته، از پورت جدا می‌شه.
> برای اینکه سرور بتونه چندین بسته رو دریافت کنه بدون اینکه قطع بشه، باید از گزینه `-k` استفاده کنی.

# TCP
server
```bash
nc -l -k localhost 1122

//short modle is
nc -l -k 1122

```
client
```bash
nc localhost 1122
```


![[Screenshot from 2025-01-02 10-46-18.png]]
# UDP
server
```bash
nc -lu -k localhost 1122

//short modle is
nc -lu -k 1122

```
client
```bash
nc -u localhost 1122
```
