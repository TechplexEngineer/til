Manually send an HTTP request with netcat (NC)
======


```bash
cat <<EOF | nc example.com 80
GET / HTTP/1.1
Host: example.com

EOF
```

[Ref](https://riptutorial.com/http/example/5252/sending-a-minimal-http-request-manually-using-telnet)
