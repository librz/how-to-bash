`find` walks a file directory to find files

`find` is an old tool in that:

- `find` uses single dash instead of double dash (such as `-name` instead of `--name`)
- `find` doesn't suport `a=b` (such as `-maxdepth=2` is not suported)

### baisc usages

- `find ~ -name '.zshrc'` find by exact name of file/folder
- `find /var/www -name '*.html'` find files/folders whose name ends with `html`
- `find . ! -name '*.txt'` find items whose name doesn't ends with `.txt`
- `find . -maxdepth 2 -name '*.js'` limit maxdepth to 2
- `find . -iname '*react*'` find items whose name contains `react`, case-insensitive
