`find` walks a file directory to find files/folders

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
- `find . -type f -size 2k` find files whose size >= 2KB (`2k` means `>=2KB`; `+2k` means >2KB; `-2k` means <2KB. Other than `k` you can also specify `M`, `G` to mean MB, GB respectively.)

### and & or

- `find ./src \( -name '*.ts' -or -name '*.js' \)`
- `find ./src \( -name '*config*' -and -type f \)`

### combine with other commands (`--exec`)

note: `find` uses `{}` to represent filenames in the `-exec` clause

- `find ~/Desktop -type f -size +10M -exec ls -lh {} \;` find files that are larger than 10MB in `~/Desktop`, list them using `ls -lh`
- `mkdir small_files && find ~/Desktop -type f -size -1M -exec copy {} small_files \;`
