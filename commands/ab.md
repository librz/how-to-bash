`ab` (ApacheBench) is an old-school HTTP benchmarking tool. It can send multiple concurrent requests to stree-test (even DoS attack) target HTTP server.

#### exampole

```sh
# send out a total of 10000 requests to google.com, with 100 requests at a time
ab -c 100 -n 10000 http://google.com
```

#### docs

https://httpd.apache.org/docs/2.4/programs/ab.html
