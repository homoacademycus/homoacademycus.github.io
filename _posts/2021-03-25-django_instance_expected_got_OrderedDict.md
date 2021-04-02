---
{"layout": "post", "categories": "TroubleShooting", "title": "django instance expected got OrderedDict", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
'Rule' instance expected, got OrderedDict([('title', 'sdfsd'), ('body', 'sdfsdf')])
```

# Cause
```
for rule in rules_data:
    Rule(
        contract_n = contract,
```

# Solution
use constructor as ModelClassname.objects.create() not ModelClassname()
```
for rule in rules_data:
    ruleObj = Rule.objects.create(
        contract_n = contract,
        **rule
    )
```
