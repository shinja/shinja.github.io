---
layout: post
title: "Python SimpleHTTPServer"
date: 2015-07-27 18:48:36
category: "Web Devilopment" 
tags: [Python, SImpleHTTPServer]
---

### Why Python SimpleHTTPServer Always return 200 for cached file?

Normally, a file without modified and `Cache-Control` is not disabled,
a HTTP server should always return 304 for indicating the file is `Not Modified`.
However, the Python http libraries does not support last-modified date checking.

See: 
http://www.diveintopython.net/http_web_services/http_features.html
http://www.bogotobogo.com/python/python_http_web_services.php#last_modified_checking

> Python's URL library has no built-in support for last-modified date checking, but since you can add arbitrary headers to each request and read arbitrary headers in each response, you can add support for it yourself.

Fortuntately, even the SimpleHTTPServer return status code as 200, it still notify the browser to get the resource from cache.

see Picture.
