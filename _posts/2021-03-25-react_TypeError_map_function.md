---
{"layout": "post", "categories": "TroubleShooting", "title": "react TypeError map function", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
Uncaught TypeError: someState.map is not a function

TypeError: Object doesn't support property or method {x} (Edge)
TypeError: "x" is not a function
```

# Cause
```
.map() is function for Array.

The JavaScript exception "is not a function" occurs when there was an attempt to call a value from a function, but the value is not actually a function.
```

# Solution
```
check someState is Array or not.
```

