
## Talk two server
```bash
Client
ssh -R 1080:localhost:1080 root@xxx.xxx.xx.xx
nc -l -p 1080

Server
ssh root@xxx.xxx.xxx.xxx
nc localhost 1080

echo "Hello from the server" | nc localhost 1080


curl --socks5 127.0.0.1:1080 icanhazip.com
curl --proxy 127.0.0.1:1080 icanhazip.com
```


other
```bash
python3 -m http.server 1122
curl --proxy http://localhost:1122 http://example.com

```