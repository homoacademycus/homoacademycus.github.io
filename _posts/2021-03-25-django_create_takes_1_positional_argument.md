---
{"layout": "post", "categories": "TroubleShooting", "title": "django create takes 1 positional argument", "feature-img": "assets/img/feature_img.png"}
---
# Symtom
```
create() takes 1 positional argument but 2 were given
```

# Cause
```
Rule.objects.create(contract, **rule)
return getattr(self.get_queryset(), name)(*args, **kwargs)
```

# Solution
```
for rule in rules_data:
            Rule(
                contract_n = contract['contract_n'],
                title = rule['title'],
                body = rule['body']
            )
```
write each field as explicit
