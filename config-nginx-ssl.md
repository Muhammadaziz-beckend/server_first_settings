server {

    listen 80;
    listen [::]:80;


    listen 443 ssl;
    listen [::]:443 ssl;
    server_name smarthouse.website www.smarthouse.website;
    # Сертификат:
	ssl_protocols TLSv1.2;
    ssl_certificate /etc/ssl/smarthouse.website2.crt;
    ssl_certificate_key /etc/ssl/smarthouse.website2.key;

location / {
    proxy_pass http://localhost:5174;
    proxy_read_timeout 120;
    proxy_connect_timeout 120;
    proxy_send_timeout 120;
    proxy_redirect off;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}

location /service-worker.js {
        root /var/www/control_work/front/public;
        try_files $uri $uri/ =404;
    }


    location /static/ {
        alias /var/www/control_work/beck/staticfiles/;
    }

    location /media/ {
        alias /var/www/control_work/beck/media/;
    }

    # Настройки для API бекенда
        location /api/ {
        proxy_pass http://127.0.0.1:8000/api/;
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

    location /admin/ {
        proxy_pass http://127.0.0.1:8000/admin/;
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
