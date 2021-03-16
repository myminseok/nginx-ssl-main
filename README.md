# This is for ssl test on nginx.


# generate domain certs.

```
git clone https://github.com/myminseok/nginx-ssl-main

cd nginx-ssl-main

git submodule update

cd generate-self-signed-cert

vi openssl-root.conf

vi openssl-root.conf

generate.sh
```



test the certificate with nginx
```
cd nginx-ssl-main

docker-compose up

open https://test.com/
```

