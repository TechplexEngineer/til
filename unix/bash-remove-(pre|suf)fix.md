Remove variable prefix or suffix
================================

```bash
string="/var/log/nginx.log";
prefix="/var/log/";
string=${string#$prefix}; #Remove prefix
echo $string; #Prints "nginx.log"

suffix=".log";
string=${string%$suffix}; #Remove suffix
echo $string; #Prints "nginx"
```

[Source](https://bytefreaks.net/gnulinux/bash/how-to-remove-prefix-and-suffix-from-a-variable-in-bash)
