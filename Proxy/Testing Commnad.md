
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