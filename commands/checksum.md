Checksum is a way of file integrity verification using hash algorithms.

There are many ways of generating checksums, the most popular ones are `md5` `sha1` & `sha256`

#### md5

on macOS, the command is `md5`; on Linux, it's `md5sum`

it produces a 128-bit checksum which is 32 characters in hex

usage:

```sh
md5sum {{ filename }} # generate md5 checksum of a file
echo "something" | md5sum # generate md5 checksum from stdin
```

### sha

on both macOS & Linux, the command is `shasum`

sha1 is the first version of sha, it produces a 160-bit checksum(40 characters in hex). 

Git use sha1 internally, that's why commit id is always 40 characters.

sha2 is a family of hash algorithms, the most famous one is sha256, as its name suggest, it produces a 256-bit checksum(64 characters in hex).

usage:

```sh
shasum {{ filename }} # by default shasum generates sha1 checksum
shasum -a 1 {{ filename }} # explicitly using sha1
shasum -a 256 {{ filename }} # use sha256
echo "something" | shasum # generate shasum from stdin
```

---

reference: https://www.freecodecamp.org/news/md5-vs-sha-1-vs-sha-2-which-is-the-most-secure-encryption-hash-and-how-to-check-them/
