`tar` is an archive & compress utility

#### options

`tar` has several options and u can combine them together, namely:

1. `c` for create
2. `g` for gzip
3. `x` for extract(unarchive)
4. `t` for list
5. `f` for file, seems to be always needed

### list contents of an archive

`tar tf path/to/archvie`

### archive

1. create an archive file from several files: `tar -cf path/to/target.tar path/to/file1 path/to/file2 ...`
2. create a gzipped archive file: `tar -cgf path/to/target.tar path/to/file1 path/to/file2 ...`
3. create an archive file of an directory: `tar -cf path/to/target path/of/archive`
### extract (unarchive)

`tar -xf path/to/archive -C path/of/extracted_files`

in case of tar bomb where a tar file directly contains a lot of file, it's recommendated to create a temp folder first, then put the extracted files in it
