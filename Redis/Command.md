
Config redis server

```bash
sudo vi /etc/redis/redis.conf

- `bind 0.0.0.0`
- `requirepass your_redis_password`

sudo systemctl restart redis-server

```



connect to server
```bash
edis-cli -h XXX.XXX.XXX.XXX -p 6379
AUTH CLIENT_PASSWORD


```


```bash
edis-cli -h XXX.XXX.XXX.XXX -p 6379 --pass CLIENT_PASSWORD
```

> [!WARNING]
> Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
> 

## python
```bash
pip install redis


import redis

# اتصال به Redis
client = redis.StrictRedis(host='127.0.0.1', port=6379, decode_responses=True)

# تست اتصال
print(client.ping())  # خروجی باید True باشد

```

