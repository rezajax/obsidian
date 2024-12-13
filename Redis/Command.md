
Config redis server

```bash
sudo vi /etc/redis/redis.conf

- `bind 0.0.0.0`
- `requirepass your_redis_password`

sudo systemctl restart redis-server

```



connect to server
```bash
edis-cli -h 172.245.67.162  -p 6379
```


