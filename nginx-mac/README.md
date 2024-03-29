# This is for SSL cert test on nginx.


## Generate domain certs.

```
git clone https://github.com/myminseok/nginx-ssl-main

cd nginx-ssl-main

git submodule update
or 
git clone  https://github.com/myminseok/generate-self-signed-cert.git

cd generate-self-signed-cert


vi openssl-domain.conf

generate.sh
```

optional) make certificate bundle (for nginx only. the domain cert should be at last)
```
cat root.crt domain.crt > bundle.crt
```

## Prepare backend app(http)

run any app using http protocol

test 
```
curl http://localhost:8080
```

## Using brew nginx on Mac

```
brew install nginx
```

edit nginx-mac/nginx.conf

copy nginx.conf
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


edit /etc/hosts
```
vi /etc/hosts
127.0.0.1 test.com
```

test app
```
curl https://test.com
```

