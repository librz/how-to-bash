### the first line of your script should alwyas be shabang

```bash
#!/bin/bash
```

`#!` is called shabang

it should be literally the FIRST line, top of your script file. If you put it in second line and leave the first line empty, it won't work

### alwyas check bash script using `shellcheck` before running it

shellcheck is a reliable static analyzer for shell scripts, it detects potential issues within your script & produce warnings.

```bash
shellcheck /path/to/script
```

[install shellcheck](https://github.com/koalaman/shellcheck)

### use tldr to list the most common usages of a command

```bash
# find out how to use tar
tldr tar
```

[install tldr](https://github.com/tldr-pages/tldr)

I use tldr because man pages are long-winded, but I still use man becuase it's more comprehensive

### use [explainshell](explainshell.com) to interpret & understand commands

```bash
curl -sL https://google.com
```

copy this line into explainshell.com's search box and see what happens
