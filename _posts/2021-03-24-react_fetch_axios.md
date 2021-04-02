---
{"layout": "post", "categories": "TroubleShooting", "title": "react fetch axios", "feature-img": "assets/img/feature_img.png"}
---
# fetch
```
let url = 'https://someurl.com';
let options = {
            method: 'POST',
            mode: 'cors',
            headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json;charset=UTF-8'
            },
            body: JSON.stringify({
                property_one: value_one,
                property_two: value_two
            })
        };
if (response && response.ok) {
    let jsonData = await fetch(url, options).json(); //responseObj.json()
}
```
- included in react by default (don't have to care about module update issue)
- no response timeout API provided
- not supported with some browser
- whend error catched --> always execute .then()

# axios
```
let url = 'https://someurl.com';
let options = {
            method: 'POST',
            url: url,
            headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json;charset=UTF-8'
            },
            data: {
                property_one: value_one,
                property_two: value_two
            }
        };
if (response && response.status === 200 && response.statusText === 'OK') {
    let jsonData = await axios(options).data; //responseObj.data
}
```




