base64 is a neat command for enocding to & decoding from base64 string

#### syntax

```bash
# encode to base64 string
base64 --input=filename

# decode from base64 string
base64 --decode --input=filename
```

#### example

```bash
# imgage -> base64 string (filename: avatar.png)
base64 --input=avatar.png

# base64 string -> image
base64 --decode --input=[base64string] > avatar.png
```

#### why a string representation of files are import

For example, instead of referencing a remote url, you can embed image directly in html as string using data url. 

![image](data:image/png;base64,<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>)

This guarantees the embedded image show up immedately after the html file is loaded.

#### why use base64, not binary or hex?

There are many ways you can stringify a file

Since all files are stored in computer as binary, using binary string is obvious a possible solution.

But it has a caveat, using binary, every bit requires a corresponding '0' or '1', resulting a long-winded string.

Using hex condenses every 4 bit(four '0's & '1's) to 1 char, dramatically reduces the length of generated string.

But still it's not concise enough, duplication remains.

Base64 analyses input & optimize for less duplication, resulting in a relative short string compared to binary or hex.
