Make network namespaces visible to the ip command
=================================================

 Docker creates its namespace objects in /var/run/docker/netns, but iproute2 expects to find them in /var/run/netns.


### TLDR
```sudo ln -s /var/run/docker/netns /var/run/netns```


### Example
```
$ sudo ls -l /var/run/docker/netns  
 total 0  
 -r--r--r--. 1 root root 0 Feb 1 11:16 1-6ledhvw0x2  
 -r--r--r--. 1 root root 0 Feb 1 11:16 ingress_sbox  
 $ sudo ip netns list  
 $ sudo ln -s /var/run/docker/netns /var/run/netns  
 $ sudo ip netns list  
 1-6ledhvw0x2 (id: 0)  
 ingress_sbox (id: 1)  
 $  
 ```
 
 [ref](https://www.fragmentationneeded.net/2017/02/)
