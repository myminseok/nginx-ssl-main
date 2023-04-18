# This is for SSL cert test on nginx.


# generate domain certs.

```
git clone https://github.com/myminseok/nginx-ssl-main

cd nginx-ssl-main

git submodule update
or 
git clone  https://github.com/myminseok/generate-self-signed-cert.git

cd generate-self-signed-cert

vi openssl-root.conf

vi openssl-domain.conf

generate.sh

make certificate bundle (for nginx only. the domain cert should be at last)
cat root.crt domain.crt > bundle.crt
```

# prepare backend app(http)

run any app using http protocol

test 
```
curl http://localhost:8080
```

# Using docker-compose


RUN nginx with the certificate
```
cd nginx-ssl-main

docker-compose up

```
test
```
vi /etc/hosts
127.0.0.1 test.com
```


```
openssl s_client -connect test.com:443

CONNECTED(00000003)
depth=1 C = KR, O = MyCA, CN = root Self Signed CA
verify error:num=19:self signed certificate in certificate chain
verify return:0
---
...
```

## Using brew on Mac

```
brew install nginx
```

edit nginx.conf

```
vi nginx-mac/nginx.conf
```

```
events {
    worker_connections  1024;
}
http {
  server {
    listen 443 ssl;
    server_name test.com
    ssl on;
    ssl_certificate     /PATH/TO/nginx-ssl-main/generate-self-signed-cert/domain.crt;
    ssl_certificate_key /PATH/TO/nginx-ssl-main/generate-self-signed-cert/domain.key;
     ssl_prefer_server_ciphers off;
    location / {
      proxy_pass http://127.0.0.1:8080;
    }
  }
}
```
copy nginx.conf to 
```
cp nginx-mac/nginx.conf /opt/homebrew/etc/nginx/nginx.conf
```

test nginx.conf
```
nginx -t


nginx: the configuration file /opt/homebrew/etc/nginx/nginx.
conf syntax is ok
nginx: configuration file /opt/homebrew/etc/nginx/nginx.conf test is successful
```

start nginx
```
nginx -s stop
nginx

```

reload conf
```
nginx -s reload
```

