# DIALOG

# ENVIRONMENT
Нужен [python3](./env.md)

## Setup
npm install

## Setup launch

Добавить в package.json, секция скриптов

```
"prod": "MEDIASOUP_LISTEN_IP=___INTERNAL_IP__ MEDIASOUP_ANNOUNCED_IP=___EXTERNAL_IP___ HTTPS_CERT_FULLCHAIN=/etc/letsencrypt/live/hubs3.arvr.sberlabs.com/fullchain.pem HTTPS_CERT_PRIVKEY=/etc/letsencrypt/live/hubs3.arvr.sberlabs.com/privkey.pem DOMAIN=hubs3.arvr.sberlabs.com node index.js"

```

# Launch

Тестовые запуски для посомтра проблем запуска

```npm run prod```

Продуктивные - **через менеджеры node js скриптов (forever/pm2)**, с '&' примерно через час процесс погибнет



