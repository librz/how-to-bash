The `grep` utilit searches any given input(s), selecting lines that match one or more patterns.

#### Basic Usage

```sh
# search for lines that includes "scripts" (case sensitive) and print them
grep "scripts" package.json
# or
cat package.json | grep "scripts"

# search for lines that includes "scripts" (case insensitive) and print them
grep -i "scripts" package.json

# print 3 lines of context around each match
grep --content=3 "scripts" package.json
# print 5 lines of context before each match
grep --before-content=5 "scripts" package.json
# print 2 lines of context after each match
grep --after-content=5 "scripts" package.json
```
