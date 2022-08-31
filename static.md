# STATIC BUILDS

# HUBS
## SETUP
Зависимости не выкачиваются, я поправил в своей [репе](https://github.com/Shadowru/hubs) 

Исправить .default.env

```
RETICULUM_SERVER="https://HOST_NAME"
BASE_ASSETS_PATH="https://HOST_NAME:8080/"
```

Каталог dist указать в конфиге [NGINX](./nginx.md) - секция порта 8080

## BUILD

```
npm run build
```

# HUBS ADMIN
Репо HUBS/admin/ 
Исправить .default.env

```
POSTGREST_SERVER="https://HOST_NAME/api/postgrest"
BASE_ASSETS_PATH="https://HOST_NAME:8989/"
```

## BUILD
```
npm run build
```

Каталог dist указать в конфиге [NGINX](./nginx.md) секция порта 8989

# SPOKE

Запоротые стили, не собирается, я поправил в своей [репе](https://github.com/Shadowru/Spoke)

Исправить .env.prod

```
HUBS_SERVER="HOST_NAME"
RETICULUM_SERVER="HOST_NAME"
FARSPARK_SERVER="farspark.reticulum.io"
CORS_PROXY=""
NON_CORS_PROXY_DOMAINS="HOST_NAME:4000,reticulum.io"
ROUTER_BASE_PATH="/spoke"
IS_MOZ="false"
CORS_PROXY_SERVER=""
BASE_ASSETS_PATH="https://HOST_NAME:9090/"
```

## BUILD
```
npm run build
```

Каталог dist указать в конфиге [NGINX](./nginx.md) секция порта 9090
