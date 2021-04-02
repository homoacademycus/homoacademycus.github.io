---
{"layout": "post", "categories": "TroubleShooting", "title": "django direct assignment to reverse related set", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
Direct assignment to the reverse side of a related set is prohibited.
Use related.set() instead.
```

# Cause
```
class Meta:
        model = Contract
        fields = [ ... , 'related']
rules_data = validated_data.pop('rules')
contract = Contract.objects.create(**validated_data)
getattr(self.get_queryset(), name)(**args, **kwargs)
```

# Solution
필드를 일일이 지정하고, 따로 빼서 set() 으로 대입해보니
```
contract = Contract.objects.create(
            name = validated_data['name'],
            email = validated_data['email'],
            date_from = validated_data['date_from'],
            date_to = validated_data['date_to']
        )
contract.related.set(validated_data.related)
```
set() 메소드에서 에러가 나서 보니
```
'dict' object has no attribute 'related'
```
리스트로 감싸서 제공
```
contract.related.set(validated_data['related'])
```
