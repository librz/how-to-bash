

### sed

all examples given uses gnu sed, if you are using a mac, you may want to install gsed `brew install gsed`


basic usage, find & replace:

```sh
# the begining 's' in 's/some/we/' means substitute 
echo "some believes in religion, some believes in science, while some believes in instinct" | sed 's/some/we/'
```

replace all occurence 

```sh
# g at the end meansing Global match
echo "some believes in religion, some believes in science, while some believes in instinct" | sed 's/some/we/g'
```

file as input (without chaning file)

```sh
echo "some believes in religion, some believes in science, while some believes in instinct" > test.txt
sed 's/some|we/g' test.txt
```

fiel as input (change file in place)

```sh
echo "some believes in religion, some believes in science, while some believes in instinct" > test.txt
sed -i 's/some/we/g'
```


