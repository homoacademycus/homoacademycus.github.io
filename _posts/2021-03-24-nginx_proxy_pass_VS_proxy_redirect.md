---
{"layout": "post", "categories": "TroubleShooting", "title": "nginx proxy pass VS proxy redirect", "feature-img": "assets/img/feature_img.png"}
---
# proxy_redirect 
changing the Location response header in a 3xx status message.

rewrite statement does nothing 
other than prevent further modification of the URI. 
This line needs to be deleted 
otherwise it will inhibit proxy_pass from mapping the URI.

# proxy_pass
map the URI (e.g. from /api/path to /path) 
by appending a URI value to the proxy_pass value, 
which works in conjunction with the location value
```
location /api {
    proxy_pass http://another-IP:port/api;
}
```

You may need to set the Host header only if 
your upstream server does not respond correctly 
to the value another-IP:8080.

You may need to add one or more proxy_redirect statements 
if your upstream server generates 3xx status responses 
with an incorrect value for the Location header value.

