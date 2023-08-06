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
grep --context=3 "scripts" package.json
# before context
grep --before-content=3 "scripts" package.json
# after context
grep --after-content=3 "scripts" package.json

# --context=n can be also written as -Cn
# likewise --before-context=n -> -Bn; --after-context=n -> -An
```
