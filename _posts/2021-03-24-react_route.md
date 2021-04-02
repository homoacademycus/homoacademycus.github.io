---
{"layout": "post", "categories": "TroubleShooting", "title": "react route", "feature-img": "assets/img/feature_img.png"}
---
# history stack - HTML5 history API (pushState, replaceState)
```
Home > One > Two
```

# history.push('/new')
```
Home > One > Two > new
```

# history.replace('/new')
```
Home > One > new
```

# location - return current URL state
```
function usePageViews() {
  let location = useLocation();
  React.useEffect(() => {
    ga.send(["pageview", location.pathname]);
  }, [location]);
}
```
whenever a new page loads, trigger a new “page view” event

# useParams - return url parameters as key/value pair
```
let { postid } = useParams();
<Route path="/post/:postid" component={post} />
```

# useRouteMatch - access to match data without actually rendering a <Route>
```
let match = useRouteMatch("/post/:postid");
```

# <Redirect to="/new" />
```
Home > One > new
```
override the current location in the history stack, 
like server-side redirects (HTTP 3xx) do.

# <Link to="/new replace={true} />
```
Home > One > new
```
override the current location in the history stack


