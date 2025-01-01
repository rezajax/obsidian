# Server
version ()
```toml
[common]
bind_port = 7000
vhost_http_port = 8080
vhost_https_port = 443


# rez: working properly.
dashboard_port = 7500
dashboard_user = admin
dashboard_pwd = admin

# rez: this is not working.
[webServer]
addr = "0.0.0.0"
port = 7500
user = "admin"
password = "admin"
                                                                   
~                                             
```

## run server
```bash
./frps -c frps.toml
```

# Client
version 0.61.1 (isntalled with pkg)
```toml

serverAddr = "107.175.73.102"
serverPort = 7000

[[proxies]]
name = "test-tcp"
type = "tcp"
localIP = "127.0.0.1"
localPort = 1888
remotePort = 1888

[[proxies]]
name = "test-udp"
type = "udp"
localIP = "127.0.0.1"
localPort = 1888
remotePort = 1888



```
## run client
```bash
frpc -c frpc3.toml
```

---
