https://chatgpt.com/share/6777106b-c14c-8013-ae11-141076c7a94d



```bash
sudo iptables -t nat -A PREROUTING -p udp --dport 1080 -j DNAT --to-destination 192.168.1.227:1080
sudo iptables -t nat -A POSTROUTING -p udp -d 192.168.1.227 --dport 1080 -j MASQUERADE

```


```bash

sudo iptables -t nat -A PREROUTING -p udp --dport 1080 -j REDIRECT --to-port 1080 
sudo iptables -A FORWARD -p tcp --dport 1080 -j ACCEPT
```