---
{"layout": "post", "categories": "TroubleShooting", "title": "react undefined map function", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
Uncaught TypeError: *** is not a function in a React component
or
someState.map is undefined
```

# Cause
```
someState Array data is not loaded before rendering.
```

# Solution
render components with states after data is all loaded.
```
const [ loadState, setLoadState ] = React.useState(true);
React.useEffect( () => {
    setLoadState(true);
    setDataState(data);
    setLoadState(false);
},[]);
if (loadState == true){
    return( <>loading...</>);
}
return( 
    ...render components...
);
```

