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

```

make certificate bundle (for nginx only. the domain cert should be at last)
```
cat root.crt domain.crt > bundle.crt
```


# RUN nginx with the certificate
```
cd nginx-ssl-main

docker-compose up

```

# test
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
Certificate chain
 0 s:/C=KR/O=MyOrg/OU=MyOrg/CN=test.com
   i:/C=KR/O=MyCA/CN=root Self Signed CA
 1 s:/C=KR/O=MyCA/CN=root Self Signed CA
   i:/C=KR/O=MyCA/CN=root Self Signed CA
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIDcjCCAlqgAwIBAgIJAIBsOfJJPa48MA0GCSqGSIb3DQEBCwUAMDoxCzAJBgNV

SJuC7tkstafn/ecivOyH2awDdehAMQ==
-----END CERTIFICATE-----
subject=/C=KR/O=MyOrg/OU=MyOrg/CN=test.com
issuer=/C=KR/O=MyCA/CN=root Self Signed CA
---
No client certificate CA names sent
Server Temp Key: ECDH, X25519, 253 bits
---
SSL handshake has read 2279 bytes and written 289 bytes
---
New, TLSv1/SSLv3, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated

```

