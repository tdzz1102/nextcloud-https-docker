# nextcloud-https-docker

A nextcloud image that enables https.

公式イメージ`nextcloud:latest`から派生し、httpsを有効化したnextcloudイメージ。

[view on dockerhub](https://hub.docker.com/r/kakusi/nextcloud/tags)

## 使い方

自分で証明書を発行

```
openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout key.pem -out cert.pem
```

コンテナ起動

```bash
docker run -d -p 8080:80 -p 8443:443 \
  -v nextcloud:/var/www/html \
  -v /your/cert:/cert/cert.pem \
  -v /yout/cert_key:/cert/key.pem \
  -e http_proxy=http://your.proxy:2023 \
  -e https_proxy=http://your.proxy:2023 \
  kakusi/nextcloud:https
```

コンテナ80番ポートはhttpで、443番ポートはhttpsを使います。`http_proxy`と`https_proxy`が要らない場合は`-e http_proxy=`と`https_proxy`をそのまま置く必要があります。
