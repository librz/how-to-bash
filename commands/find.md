`find` walks a file directory to find files

`find` is an old tool in that:

- `find` uses single dash instead of double dash (such as `-name` instead of `--name`)
- `find` doesn't suport `a=b` (such as `-maxdepth=2` is not suported)

### find by name

- `find ~ -name '.zshrc'` find by exact name of file/folder
- `find /var/www -name '*.html'` find items whose name ends with `html`
- `find . ! -name '*.txt'` find items whose name doesn't ends with `.txt`
- `find . -iname '*react*'` find items whose name contains `react`, case-insensitive


### specify `maxdepth`, `type`, `size`

- `find . -maxdepth 2 -name '*.js'` limit maxdepth to 2
- `find . -type f -name '*js*'` find files that contian `js` (`f` for file; `d` for directory)
- `find . -type f -size 2k` find files whose size >= 2KB (`2k` means `>=2KB`; `+2k` means >2KB; `-2k` means <2KB. Other than `k` you can also specify `k`, `M`, `G` to mean KB, MB, GB respectively.)


### and & or

- `find ./src \( -name '*.ts' -or -name '*.js' \)`
- `find ./src \( -name '*config*' -and -type f \)`
