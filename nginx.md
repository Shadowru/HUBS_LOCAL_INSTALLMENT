NGINX config
```
server {
        root /var/www/html/hubs/admin/dist;

        listen [::]:8989 ssl ipv6only=on;
        listen 8989 ssl;

        add_header Access-Control-Allow-Origin https://hubs3.arvr.sberlabs.com;

        ssl_certificate /etc/letsencrypt/live/hubs3.arvr.sberlabs.com/fullchain.pem; # managed by Certbot
        ssl_certificate_key /etc/letsencrypt/live/hubs3.arvr.sberlabs.com/privkey.pem; # managed by Certbot
        include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
        ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}

server {
        root /var/www/html/hubs/dist/;

        listen [::]:8080 ssl ipv6only=on;
        listen 8080 ssl;

        add_header Access-Control-Allow-Origin https://hubs3.arvr.sberlabs.com;

        ssl_certificate /etc/letsencrypt/live/hubs3.arvr.sberlabs.com/fullchain.pem; # managed by Certbot
        ssl_certificate_key /etc/letsencrypt/live/hubs3.arvr.sberlabs.com/privkey.pem; # managed by Certbot
        include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
        ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}

server {
        root /var/www/html/spoke/dist;

        listen [::]:9090 ssl ipv6only=on;
        listen 9090 ssl;

        add_header Access-Control-Allow-Origin https://hubs3.arvr.sberlabs.com;

        ssl_certificate /etc/letsencrypt/live/hubs3.arvr.sberlabs.com/fullchain.pem; # managed by Certbot
        ssl_certificate_key /etc/letsencrypt/live/hubs3.arvr.sberlabs.com/privkey.pem; # managed by Certbot
        include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
        ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}

server {
    listen 80 default_server;
    listen [::]:80 default_server;

    server_name hubs3.arvr.sberlabs.com;

    #hubs must not serve with http, so redirect it to https
    return 301 https://$host$request_uri;
}


server {
    server_name hubs3.arvr.sberlabs.com;

     location / {
        #match everything
        rewrite ^\/(.*)$ /$1 break;
        # Proxy passing to port 4000
        proxy_pass https://hubs3.arvr.sberlabs.com:4000;
        # The Important Websocket Bits!
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";

        #Give larger upstream buffers
        fastcgi_buffers 16 16k;
        fastcgi_buffer_size 32k;
        proxy_buffer_size 128k;
        proxy_buffers 4 256k;
        proxy_busy_buffers_size 256k;
    }

    listen [::]:443 ssl ipv6only=on; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/hubs3.arvr.sberlabs.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/hubs3.arvr.sberlabs.com/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}
```
