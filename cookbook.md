1. store output of a command/script in a variable when it's successful(exit code 0)

```console
if ! result=$(bash /path/to/another/script.sh); then
	exit 1
fi

echo "$result"
```

