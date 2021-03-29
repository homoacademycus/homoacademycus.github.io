---
{"layout": "post", "categories": "TroubleShooting", "title": "nginx proxy pass VS proxy redirect", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
"proxy_redirect default" cannot be used with "proxy_pass" directive 
with variables in /etc/nginx/sites-enabled/myapp.conf
```

# Cause
- proxy_redirect
```
changing the Location response header in a 3xx status message.
it will inhibit proxy_pass from mapping the URI

use when upstream server generates 3xx status responses 
with an incorrect value for the Location header value.
```

- proxy_pass
```
map the URI (e.g. from /api/path to /path)
which works in conjunction with the location value

set the Host header when upstream server does not respond correctly 
to the proxyIP:port
```

# Solution
use only one of them
