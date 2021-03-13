---
{"layout": "post", "categories": "TroubleShooting", "title": "UnicodeDecodeError", "feature-img": "assets/img/feature_img.png"}
---
## Symtoms
```
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xc6 in position 4: invalid continuation byte
```

## Cause
```
attempting to pass in non-ASCII byte values will trigger UnicodeDecodeError.
```

## Solution
```
use encode(), decode()

Each produces a value of a corresponding type that contains either bytes data (for encode() methods) or str data (for decode() methods).
python v3.2 : URL parsing functions now accept ASCII encoded byte sequences
```


