#### check to see whether a program/command exist (if it exists, don't print out anything; if not, just exit)

```console
if ! command -v awk &> /dev/null; then 
	echo "awk is not installed on this computer"
	exit 1
fi

# don't use "which {program}" as shellcheck suggest
```

#### install a program, automatically answer "y" for every prompt during the install process

```console
# basic version
yes | apt install {program}

# you shouldn't use "echo y | apt install {program}" 
# since this only prints out "y" once and there may be multiple prompts

# usually you want to run "apt update" before install
# and sometimes in script, you don't want to print out anything
apt update &> /dev/null && yes | apt install {program} &> /dev/null
```

#### cd into the folder where the script is in, exit if it fails

```console
# I still don't understand how it works :)

if ! cd "$(dirname "${BASH_SOURCE[0]}")"; then
	echo "cd failed"
	exit 1
fi

# this allows you to run the script from elsewhere
# as if you're running the script directly from where it's stored
````

#### run a command, throw error when it fails

```console
if ! git fetch origin; then
	echo "failed to run git fetch, check your network connection"
	exit 1
fi
```

#### store output of a command/script in a variable for later use, exit if it fails

```console
if ! result=$(bash /path/to/another/script); then
	exit 1
fi

echo "$result"
```

#### prompt user for input and store it in a variable

```console
# -p stands for prompt
read -r -p "Do you want to continue? (Y/N) " answer
```

#### check if string is empty or not

```console
# you can use "-z" or "-n" to check

# -z means "Empty"
if [[ -z "$var" ]]; then
	echo "Empty"
else
	echo "Not Empty"
fi

# -n means "Not Empty"
if [[ -n "$var" ]]; then
	echo "Not Empty"
else
	echo "Empty"
fi
```

#### compare if 2 strings are the same

```console
name="John Blake"
if [[ "$name" == "John Blake" ]]; then
	echo "same"
else
	echo "not same"
fi
```

### compare if 2 numbers are equal

```console
if [[ "$age1" -eq "$age2" ]]; then
	echo "equal"
else
	echo "not equal"
fi
```

#### string pattern matching with regex

```console
# the syntax is: SATRING =~ REGEX
read -r -p "How old are you? " age
if [[ "$age" =~ ^[0-9]{1,2}$ ]]; then
	echo "your age is ${age}'
else
	echo "wrong age fromat"
	exit 1
fi

# do the famouse yes or no check
read -r -p "Are you sure? (Y/N) " answer
if [[ "$answer" =~ ^[Yy][eE]?[sS]? ]]; then
	echo "confirmed"
else
	echo "canceled"
fi
```

#### define & use a function

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
