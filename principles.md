#### the first line of your script should alwyas be:

```bash
#!/bin/bash
```

the #! is also called shabang

it should be literally the FIRST line, top of your script file. If you put it in second line and leave the first line empty, it won't work

#### alwyas check bash script using shellcheck before running it:

```bash
shellcheck /path/to/script
```

you can find out how to install shellcheck in its [github page](https://github.com/koalaman/shellcheck)

#### use tldr to list the most common usage of a command

```bash
# find out how to use tar
tldr tar
```

you can find out how to install tldr in its [github page](https://github.com/tldr-pages/tldr)

I use tldr because man pages are long-winded, but I still use man becuase it's more comprehensive

#### if you find command hard to understand, use explainshell.com

```bash
curl -sL https://google.com
```

copy this line into explainshell.com's search box and see what happens
