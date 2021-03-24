---
{"layout": "post", "categories": "TroubleShooting", "title": "django self recursive", "feature-img": "assets/img/feature_img.png"}
---
# N:M recursive 관계
```
the class to which the model is related, which works exactly the same as it does for ForeignKey, including recursive and lazy relationships.
```
- 하나의 모델 안에서 ManyToManyField 사용
```
class Person(models.Model):
    friends = models.ManyToManyField("self")
```
- symmetrical=True 속성
```
ManyToManyFields on self 에서만 사용 가능(default True)
Person 모델에 person_set 속성을 추가 안하고 symmetrical 필드로 여겨짐
intermediary 모델에서도 가능
```
- Through 모델 : 연관을 위해 DB 테이블로 암시적으로 생성됨
- Through 모델을 통한 필드는 시리얼라이저에서 Read-only 필드
```
class Person(models.Model):
    name = models.CharField(max_length=50)

class Group(models.Model):
    name = models.CharField(max_length=128)
    members = models.ManyToManyField(
        Person,
        ################### 여기 ####################
        through='Membership',
        through_fields=('group', 'person'),
    ###########################################
    )

class Membership(models.Model):
    group = models.ForeignKey(Group, on_delete=models.CASCADE)
    person = models.ForeignKey(Person, on_delete=models.CASCADE)
    inviter = models.ForeignKey(
        Person,
        on_delete=models.CASCADE,
        related_name="membership_invites",
    )
    invite_reason = models.CharField(max_length=64)
```

# 1:N recursive 관계
- 하나의 모델 안에서 foreignkey 사용하는 방법
```
models.ForeignKey('self', on_delete=models.CASCADE)
```

# reverse-관계
- 모델시리얼라이저, 하이퍼링크 모델시리얼라이저에 자동포함 안됨
- 모델 클래스에서 related_name 지정해야
```
class Track(models.Model):
    album = models.ForeignKey(Album, related_name='tracks',
```
- 시리얼라이저 필드에서 Meta의 필드명으로서 related_name 값으로 지정
```
class AlbumSerializer(serializers.ModelSerializer):
    class Meta:
        fields = ['tracks', ...]
```
- 쿼리를 위해 쿼리셋.filter() 써야
```
// OR 조건
Blog.objects.filter(
        entry__headline__contains='Lennon'
    ).filter(
        entry__pub_date__year=2008
    )
```
- 문맥이 살짝 다름 : 두 조건 Lenon AND 2008 을 모두 만족시키는 객체
```
// AND 조건
Blog.objects.filter(
        entry__headline__contains='Lennon', 
        entry__pub_date__year=2008
    )
```

