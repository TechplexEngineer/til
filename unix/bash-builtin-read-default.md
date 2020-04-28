Bash builtin read default value
===============================

Often when writing a script, one needs to prompt the user. Bash has a builtin called `read` for this very purpose.


## Print the default value out and let the user edit it
```bash
#! /bin/bash

# read flags:
# -p prompt
# -r raw input. interpret backslashes literally, rather than interpreting them as escape characters.
# -i default value
# -e Get a line of input from an interactive shell.

default=my.long.server.url.example.com
if [ -z "$URL" ]
then
	read -e -r -p "url: " -i "$default" URL
	export URL
fi
```
### Output looks like this:
```
$ ./script.sh
url: my.long.server.url.example.com
```

[Ref](https://www.computerhope.com/unix/bash/read.htm)
