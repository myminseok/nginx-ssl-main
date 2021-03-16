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

```

```
vi /etc/hosts
127.0.0.1 test.com
```

```
openssl s_client -connect test.com:443 -CAfile ./root.crt

CONNECTED(00000003)
depth=1 C = KR, O = MyCA, CN = root Self Signed CA
verify return:1
depth=0 C = KR, O = MyOrg, OU = MyOrg, CN = test.com
verify return:1
---
Certificate chain
 0 s:/C=KR/O=MyOrg/OU=MyOrg/CN=test.com
   i:/C=KR/O=MyCA/CN=root Self Signed CA
---
Server certificate
-----BEGIN CERTIFICATE-----
...
AZmiVC+jTdFk32/uhH8ksCkc9Fi8HFec4Ae47AgkNUZ40KMofvFOEwfJbElKouO/
oDIVe5XEoLMepacdo8XGV00LY43vO6XdgHFUsPuqvFDstkyrjnNVIZ3DpQfqF90h
fZ/ACEbD9MTn6vwve0p5m+uLA96C9Q==
-----END CERTIFICATE-----
subject=/C=KR/O=MyOrg/OU=MyOrg/CN=test.com
issuer=/C=KR/O=MyCA/CN=root Self Signed CA
---
No client certificate CA names sent
Server Temp Key: ECDH, X25519, 253 bits
---
SSL handshake has read 1523 bytes and written 289 bytes
---
New, TLSv1/SSLv3, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated

```

