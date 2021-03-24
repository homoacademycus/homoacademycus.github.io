---
{"layout": "post", "categories": "TroubleShooting", "title": "django unhashable type OrderedDict", "feature-img": "assets/img/feature_img.png"}
---
# Symtoms
```
unhashable type: 'collections.OrderedDict'
```

# Cause
```
relatedFieldData_dict = validated_data.pop('relatedFieldData')
contract = Contract.objects.create(**validated_data)
contract.relatedField.set(relatedFieldData_dict)

the validated data turns train_statistics into a OrderedDict(always it's a bit tricky working with nested serializers), so OrderedDicts are unhashable, so when you try to ".get" it raises an error. 
An option is to set your field train_statistics into read only.
Then in your update() method, instead of using validated_data to get train_statistics, use request.data for getting them. Do the same for create() method.
When you call your serializer, you need to pass request object as context data
SummarySerializer(data=data, context={'request':request})
```

# solution - create()
```
request = self.context['request']
train_statistics_data = request.data.get('train_statistics')
summary = Summary.objects.create(**validated_data)

for train_statistic in train_statistics_data:
    TrainStatistics.objects.create(summary=summary, **train_statistic)
return summary
```

# solution - update()
```
request = self.context['request']
instance.train_statistics =request.data.get('train_statistics', instance.train_statistics) # This line is causing problems
```
