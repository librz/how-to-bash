1. run a command, throw error when it fails

```console
if ! git fetch origin; then
	echo "failed to run git fetch, check your network connection"
	exit 1
fi
```

2. store output of a command/script in a variable, print it when it's successful, quit when it failed

```console
if ! result=$(bash /path/to/another/script.sh); then
	exit 1
fi

echo "$result"
```

3. prompt user for input and store it in a variable

```console
# -p stands for prompt
read -r -p "Do you want to continue? (Y/N) " answer
```

4. check if string is empty or not

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

5. compare if 2 strings are the same

```console
name="John Blake"
if [[ "$name" == "John Blake" ]]; then
	echo "same"
else
	echo "not same"
fi
```

6. string pattern matching with regex

```console
# the syntax is: SATRING =~ REGEX
read -r -p "How old are you? " age
if [[ ${age} =~ ^[0-9]{1,2}$ ]]; then
	echo "your age is ${age}'
else
	echo "wrong age fromat"
	exit 1
fi
```

6. define & use a function

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
