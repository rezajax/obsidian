
`ss-server -c ~/ss-config.json -v`

```json
{
    "server": "0.0.0.0",
    "server_port": 1080,
    "password": "123",
    "timeout": 600,
    "method": "aes-256-gcm"
}
```




---
# Server is PC

sudo apt install shadowsocks-libev

```bash
{
    "server":"0.0.0.0",
    "server_port":1080,
    "local_port":1080,
    "password":"123",
    "method":"chacha20-ietf-poly1305"
}

ss-server -c ~/ss-config.json -v
```


```bash
ssh -R 1080:localhost:1080 root@107.175.73.102
```

![[Screenshot_2024-12-30-02-42-19-287_com.github.shadowsocks.jpg]]

local connect:

![[Screenshot_2024-12-30-02-42-32-015_com.github.shadowsocks.jpg]]

v2ray connect:

![[Screenshot_2024-12-30-02-42-37-508_com.v2ray.ang.jpg]]


---

# Server is phone

Every proxy 


