---
{"layout": "post", "categories": "TroubleShooting", "title": "react timeout useRef", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
setTimeout in useEffect doesn't work properly
```

# Cause
```
useEffect is executed when render all page
```

# Solution
useRef as pure js object - it is stable regardless of rerendering
```
const timeout = React.useRef();
React.useEffect(() => {
        timeout.current = setTimeout(() => {
            doSomething...
        }, 1500);
        return () => {
            clearTimeout(timeout.current);
        }
}, [someArr]};
```

