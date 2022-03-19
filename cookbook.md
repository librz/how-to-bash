#### run command silently(no output) 

```bash
# simply append "&>/dev/null"
apt update &> /dev/null
# some commands have slient or quite mode by design, e.g. grep's -q option
echo "hello" | grep -q "he"
# note curl's silent mode only hides progress meter and error message, it's not fully mute
curl -s http://google.com
```

#### echo the first parameter if it exist, else echo hello as fallback

```bash 
echo "${1:-hello}"
```

#### check to see whether a program/command exist (if it exists, don't print out anything; if not, just exit)

```bash
if ! command -v awk &> /dev/null; then 
	echo "awk is not installed on this computer"
	exit 1
fi

# don't use "which {program}" as shellcheck suggest
```

#### install a program, automatically answer "y" for every prompt during the install process

```bash
# basic version
yes | apt install {program}

# you shouldn't use "echo y | apt install {program}" 
# since this only prints out "y" once and there may be multiple prompts

# usually you want to run "apt update" before install
# and sometimes in script, you don't want to print out anything
apt update &> /dev/null && yes | apt install {program} &> /dev/null
```

#### cd into the folder where the script is in, exit if it fails

```bash
# I still don't understand how it works :)

if ! cd "$(dirname "${BASH_SOURCE[0]}")"; then
	echo "cd failed"
	exit 1
fi

# this allows you to run the script from elsewhere
# as if you're running the script directly from where it's stored
````

#### run a command, throw error when it fails

```bash
if ! git fetch origin; then
	echo "failed to run git fetch, check your network connection"
	exit 1
fi
```

#### store output of a command/script in a variable for later use, exit if it fails

```bash
if ! result=$(bash /path/to/another/script); then
	exit 1
fi

echo "$result"
```

#### prompt user for input and store it in a variable

```bash
# -p stands for prompt
read -r -p "Do you want to continue? (Y/N) " answer
```

#### check if string is empty or not

```bash
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

```bash
name="John Blake"
if [[ "$name" == "John Blake" ]]; then
	echo "same"
else
	echo "not same"
fi
```

### compare if 2 numbers are equal

```bash
if [[ "$age1" -eq "$age2" ]]; then
	echo "equal"
else
	echo "not equal"
fi
```

#### string pattern matching with regex

```bash
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

#### do case insensitive regex match

```bash
# there's no straightforward to ignore case using "=~"
# we'll just use grep's -i option
read -r -p "How are you doing? " answer
if echo "$answer" | grep -Ei 'good|ok|fine|well' >& /dev/null; then
	echo "Good to hear"
fi
```

#### define & use a function

```bash
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

#### write multilined text into a file

```bash
# bash uses "heredoc" to represent mutlilined text
# below is an example, for detailed explaination, just google it

cat > /path/to/file << EOF
Hi John,
	I'm only writing to check whether you have time this Sunday afternoon for a quick chat.
	Hope all is well.
Regards
EOF
```

#### write multilined text into a variable

```bash
# again, use heredoc
email=$(
cat << EOF
Hi John,
	I'm only writing to check whether you have time this Sunday afternoon for a quick chat.
	Hope all is well.
Regards
EOF
)
```
#### use for loop

```bash
for (( i=1; i<=10; i++ ))
do
	echo "Current Number: ${i}"
done
```

#### source all scripts under a folder (say ./utils)

```bash
for f in ./utils/*.sh
do
	source "$f"
done
```
