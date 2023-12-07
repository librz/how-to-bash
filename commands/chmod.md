In linux, file/directory has 3 modes, they are Readable(r), Writable(w) & Executable(x). 

|         | File                    | Directory                    |
|---------|-------------------------|------------------------------|
| Read    | read the file           | list files inside            |
| Write   | edit the file           | create & delete files inside |
| Execute | run the file as program | change to the directory      |

The `ls -l` will list file permissions as the first column, e.g.

```markdown
-rw-r--r--@  1 bytedance  staff   647K Nov  9 13:10 avatar.png
-rw-r--r--@  1 bytedance  staff   1.1M Nov  6 19:24 build.1.1.18.tar.gz
drwxr-xr-x@ 10 bytedance  staff   320B Oct 31 21:23 dist
```

Take `drwxr-xr-x` for example, the `d` in the begining means it's a directory. The rest `rwxr-xr-x` can be separated into 3 segments:

- `rwx`: permission of current user (in this case, can Read, Write & Execute)
- `r-x`: permission of user group (in this case, can Read, Execute but cannot Write)
- `r-x`: permission of other

`chmod` can be used to change file/directory permissions.

#### Basic 

`chmod [augo][+-][rwx] {file}`

e.g.

```sh
chmod u+x {file} # add file execute permission for current user
chmod g+w {file} # add file write permission for the user group of current user
chmod a+rx {file} # add file read/execute permission for all
```

