Dual-hosting DNS
================

To prevent DNS issues related to outages at a [specific provider](https://en.wikipedia.org/wiki/2016_Dyn_cyberattack) 
many orginizations choose to host their DNS records at two different unrelated providers.

Companies have created a number of options:
- [Netflix](https://medium.com/netflix-techblog/active-active-for-multi-regional-resiliency-c47719f6685b)'s [Denominator](https://github.com/Netflix/denominator)
- [StackExchange](https://blog.serverfault.com/2017/04/11/introducing-dnscontrol-dns-as-code-has-arrived/)'s [DNSControl](https://github.com/StackExchange/dnscontrol)
- [GitHub](https://githubengineering.com/enabling-split-authority-dns-with-octodns/)'s [OctoDNS](https://github.com/github/octodns)
- [Men & Mice](http://info.menandmice.com/blog/secure-your-dns-across-multiple-dns-service-platforms-with-men-mice-xdns-redundancy)'s commercial [xDNS](https://www.menandmice.com/wp-content/uploads/2017/06/Menandxdns-2.pdf)
- [HashiCorp](https://www.hashicorp.com/blog/terraform-announcement)'s [Terraform](https://github.com/hashicorp/terraform)



[Source](https://stackoverflow.com/a/47123907/429544)
