Get nameservers for a domain
====


```bash
# get NS records for $domain by recursivly removing the first section of the domain
# _acme-challenge.techplex.service.example.com
# techplex.service.example.com
# service.example.com
# example.com
while ! servers=$(dig "$domain" NS +nocomments | grep NS | grep -v ";" | awk '{ print $5 }' | sort)
do
  # strip off everything up to and including the first dot (.)
  domain=${domain#*.}
done

for ns in $servers
do
  echo "$ns"
  dig @"$ns" -t TXT "$NAME" | grep "$KEY"
done
```
