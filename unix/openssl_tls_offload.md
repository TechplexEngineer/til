Offload TLS/SSL to openssl s_client
====

Unfortunatley we needed to do this as our openssl was compiled against nss and not openssl.

```
#!/bin/bash

NAME=example.com
KEY="XKrxpRBosdIKFzxW_CT3KLZNf6q0HG9i01zxXp5CPBs"
host=certgo.service.example.com

rm fifo || true
mkfifo fifo

nc -l 8081 <fifo | openssl s_client \
        -connect $host:443 \
        -cert chain.pem -quiet \
        -key cert.key >fifo &

curl --silent -H "Host: $host" "http://localhost:8081/dns?hostname=$NAME&acmeChallengeKey=$KEY"

rm fifo
```
