1. run a command, throw error when it fails

```console
if ! git fetch origin; then
	echo "failed to run git fetch, check your network connection"
	exit 1
fi
```

2. store output of a command/script in a variable, print it when it's successful(exit code 0)

```console
if ! result=$(bash /path/to/another/script.sh); then
	exit 1
fi

echo "$result"
```

3. check if string is empty or not

```console
if [[ -z "$var" ]]; then
	echo "Empty"
else
	echo "Not Empty"
fi

# or you could use -n

if [[ -n "$var" ]]; then
	echo "Not Empty"
else
	echo "Empty"
fi
```

4. define & use a function

```console
# function without parameter
function hello {
	echo "hello world "
}
hello

# function with parameter(s)
function hi {
	echo "Hi, $1"
}
hi Lisa
```
