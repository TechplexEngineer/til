Script must be run as root
==========================

Add this snippet to ensure the script can only be run as root


```bash
if ! [ $(id -u) = 0 ]; then
   echo "Program must be run as root"
   exit 1
fi
```
