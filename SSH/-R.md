
```bash
ssh -R 80:localhost:8080 root@x.x.x.x

```



**فعال‌سازی فورواردینگ پورت در سرور (SSH Server)** در سرور، باید مطمئن شوید که فورواردینگ پورت از طرف SSH اجازه داده شده است. برای این کار باید فایل پیکربندی SSH (`/etc/ssh/sshd_config`) را ویرایش کنید و خط زیر را به آن اضافه کنید یا مطمئن شوید که فعال است:



```bash
GatewayPorts yes
```

این تنظیم باعث می‌شود که پورت‌های فوروارد شده در دسترس همه آدرس‌ها (از جمله 0.0.0.0) قرار گیرند.
