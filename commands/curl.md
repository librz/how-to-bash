cURL is a URL client written in C to download/upload data, hence the name. It supports lots of protocols with HTTP being the most fammous/
### common usages

- get help: `curl --help`
- basic usage: `curl https://www.google.com` (by default, curl will output to stdout)
- specify download filename: `curl https://www.google.com -o google.html`
- use name as indicated by url: `curl -O http://www/google.com`
- auto redirect: `curl -L google.com` (by default, curl won't auto redirect, try run `curl google.com`)
- silent mode: `curl -s https://www.google.com` (by default, curl will show progress meter if target file took some time to download, it will also show error message when error occurs, silent mode disables this)
- simple progress bar: `curl --progress-bar -OL {video_address}` (show a simple progress bar instead of detailed progress meter)

### working with HTTP

- include response headers: `curl -i https://example.com`
- send data (using POST & encoded URL): `curl -d 'name=admin&shoesize=12' http://example.com/` (No need to explicitly set request method to `POST` as it's the default method when `-d` is used. Likewise, no need to set the `Content-Type` request header to `application/x-www-form-urlencoded` when `-d` is used)
- send data (using POST & json): `curl -d '{"name":"john"}' -H 'Content-Type: application/json' https://example.com` (`-H` is used to set request header)
- send data (using PUT & json): `curl -X PUT -d '{"name":"john"}' -H 'Content-Type: application/json' https://example.com` (`-X` is used to set request method)

### Reference

[Everything CURL](https://everything.curl.dev/http/post)
