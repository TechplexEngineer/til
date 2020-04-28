grep print out after match
==========================

Sometimes when extracting text with grep it is useful to only print out part of what matched. 

> GNU grep has the -P option for perl-style regexes, and the -o option to print only what matches the pattern.

```bash
#!/bin/bash

var="foobar bash 1
foobar happy
"

echo "$var" | grep -oP 'foobar \K\w+'
```

### output:
```
bash
happy
```

[REF](https://unix.stackexchange.com/a/13472/139600)
