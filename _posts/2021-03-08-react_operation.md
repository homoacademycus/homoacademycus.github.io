---
{"layout": "post", "categories": "TroubleShooting", "title": "react operation", "feature-img": "assets/img/feature_img.png"}
---
# map is available with Array, not Set!
``` 
const tags = Array(8).fill(0).map((value, index) => (
        <StyledInput
            key={index}
            name={"binary_ip_2_"+index}
        />
)
```
- typeof( index ) == int
- typeof( string+int ) == string

# state is available with Dictionary, not Array!
```
const initState_map = {
    addr_size: "",
    files: null,
    mylist: [],
    count: 0
};
```

# make length of n Array with value
```
Array(n).fill(value)
```

# make Dictionay with map
```

```
