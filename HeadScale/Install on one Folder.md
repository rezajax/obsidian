
config.yml
```json
server {
    listen 80;
    listen [::]:80;
    server_name head.rezajax.ir;

    # Redirect HTTP to HTTPS
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name head.rezajax.ir;

    # SSL Certificates
    ssl_certificate /etc/letsencrypt/live/head.rezajax.ir/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/head.rezajax.ir/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    # Proxy to Headscale
    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_http_version 1.1;                # Required for WebSocket
        proxy_set_header Upgrade $http_upgrade; # Support WebSocket
        proxy_set_header Connection "upgrade";  # Support WebSocket
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # Prevent timeouts for WebSocket
        proxy_read_timeout 86400;
        proxy_send_timeout 86400;
    }
}

```

