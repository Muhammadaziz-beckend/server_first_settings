```
server {
    listen 80;
    listen [::]:80;
    server_name finance.smarthouse.website www.finance.smarthouse.website;

    location /static/ {
       alias /var/www/finance/staticfiles/;
    }

    location /media/ {
        alias /var/www/finance/media/;
    }

    location / {
        proxy_pass http://127.0.0.1:8006/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        client_max_body_size 65M;

        # Добавьте эти строки для увеличения таймаутов
        proxy_read_timeout 300;
        proxy_connect_timeout 300;
        proxy_send_timeout 300;
    }

}
```
