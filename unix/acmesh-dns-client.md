Implementing Acme.sh dns plugin with wget
=====

```bash
#!/bin/sh

# we will inherit settings from acmesh parent
# set -euo pipefail

CERTGO=https://certgo.service.example.com/dns
maxWaitingTimeSec=120

certchain=chain.pem
certkey=cert.key


# Usage: add  _acme-challenge.www.domain.com   "XKrxpRBosdIKFzxW_CT3KLZNf6q0HG9i01zxXp5CPBs"
# Used to add txt record
dns_certgo_add() {

        NAME=$1
        KEY=$2

	# create the chain every time in the event that the certs are changed
	cat cert.crt key.pem > $certchain

        # request dns record creation
        wget -q \
                --server-response \
                --certificate=$certchain \
                --private-key=$certkey \
                --post-data "{ \"hostname\":\"$NAME\", \"acmeChallengeKey\":\"$KEY\" }" \
                -O - \
               "$CERTGO"

        # give certgo a bit to create the records
        sleep 1

        delayIntervals=0
        while ! wget -q \
                --server-response \
                --certificate=$certchain \
                --private-key=$certkey \
                -O - \
                "$CERTGO?hostname=$NAME&acmeChallengeKey=$KEY" 2>&1 | grep "200 OK"
        do
                if [ $maxWaitingTimeSec -gt $delayIntervals ]
                then
                        break
                fi
                # this sleep must be one second or the maxWaitingTimeSec
                sleep 1
                delayIntervals++
        done

        sleep 5

        # get NS records for $domain by recursivly removing the first section of the domain
        # _acme-challenge.techplex.eaas.example.com
        # techplex.eaas.example.com
        # eaas.example.com
        # example.com
        while ! servers=$(dig "$domain" NS +nocomments | grep NS | grep -v ";" | awk '{ print $5 }' | sort)
        do
                # strip off everything up to and including the first dot (.)
                domain=${domain#*.}
        done

        for ns in $servers
        do
                echo "$ns"
                dig @"$ns" -t TXT $NAME | grep "$KEY"
        done
}

# Usage: fulldomain txtvalue
# Used to remove the txt record after validation
dns_certgo_rm() {

        NAME=$1
        KEY=$2

        # create the chain every time in the event that the certs are changed
	      cat cert.crt cert.pem > $certchain

        # request dns record creation
        wget -q \
                --server-response \
                --certificate=$certchain \
                --private-key=$certkey \
                --method=DELETE \
                --post-data "{ \"hostname\":\"$NAME\", \"acmeChallengeKey\":\"$KEY\" }" \
                -O - \
               "$CERTGO"
}
```

[Ref](https://github.com/acmesh-official/acme.sh/wiki/DNS-API-Dev-Guide)
