# Repro for issue 11482

## Steps to reproduce

1. Run `firebase hosting:channel:deploy "preview-20261110" --expires 7d --json`
```
$ firebase hosting:channel:deploy "preview-20261110" --expires 7d --json
{
  "status": "success",
  "result": {
    "aalej-fb-tools-13-test": {
      "site": "aalej-fb-tools-13-test",
      "url": "https://aalej-fb-tools-13-test--preview-20261110-51zjpow7.web.app",
      "version": "9cb36a443b59f838",
      "expireTime": "2026-11-26T11:41:12.487515681Z"
    }
  }
}
```

2. Accessing via `https://aalej-fb-tools-13-test--preview-20261110-51zjpow7.web.app/` returns the webapge
   - Note that `https://aalej-fb-tools-13-test--preview-20261110-51zjpow7.web.app/` gets converted to `https://aalej-fb-tools-13-test--preview-20261110-51zjpow7.web.app` (no slash at the end)
     - From what I can tell this behavior is something that modern browsers intentionally do
3. Run `curl -s -I -H "Accept-Encoding: gzip, deflate, br, zstd" "https://aalej-fb-tools-13-test--preview-20261110-51zjpow7.web.app/"`
   - It returns a 200 response code
```
$ curl -s -I -H "Accept-Encoding: gzip, deflate, br, zstd" "https://aalej-fb-tools-13-test--preview-20261110-51zjpow7.web.app/"
HTTP/2 200 
cache-control: max-age=3600
content-encoding: br
content-type: text/html; charset=utf-8
etag: "ddd4a858747a34157a16258dbe5649cf0c32274e1c129b8cc238e05df9588053-br"
last-modified: Thu, 19 Nov 2026 11:41:15 GMT
strict-transport-security: max-age=31556926; includeSubDomains; preload
x-robots-tag: noindex
accept-ranges: bytes
date: Thu, 19 Nov 2026 11:48:47 GMT
x-served-by: cache-mnl2150036-MNL
x-cache: HIT
x-cache-hits: 0
x-timer: S1795088927.066038,VS0,VE1
vary: x-fh-requested-host, accept-encoding
alt-svc: h3=":443";ma=86400,h3-29=":443";ma=86400,h3-27=":443";ma=86400
content-length: 103
```