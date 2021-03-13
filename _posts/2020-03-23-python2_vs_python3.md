---
{"layout": "post", "categories": "TroubleShooting", "title": "python2 vs python3", "feature-img": "assets/img/feature_img.png"}
---
# 파이썬 3 버전
* print를 일반 함수처럼 표현(괄호 필요 있음)
```
print ("Hello Python")
```

* 자동 줄바꿈 대신 end="끝 문자"로 지정 가능. default값은 '\n'
```
print ("No new line", end=" ");print ("ok?")
```

* 정수 나누기의 결과가 실수형으로 자동 형변환
```
>>> 3 / 4

0.75
```

* 파이썬 2 버전에서의 내장 함수raw_input이 input으로 바뀜
```
>>> name = input("이름을 입력하세요:")
```

* utf-8이 소스코드 인코딩의 default라 생략 가능(utf-8 이 아닌 다른 형태일 경우엔 써야)
```
# -*- coding: utf-8 -*- 
```

* 에러 처리 시 as 로 표기
```
try: 

    4 / 0 

except ZeroDivisionError as e: 

    print(e)
```
# 파이썬 2 버전
* print를 특수한 토큰처럼 표현(괄호 필요 없음)
```
print "Hello Python"
```

* 문자열의 끝에 콤마(,)를 덧불이면 자동 줄바꿈이 안됨
```
print "No new line",
print "ok?"
```

* 나누기의 결과가 실수형으로 자동 형변환 안됨 : 정수면 정수, 실수면 실수
```
>>> 3 / 4

0

>>> 3 / 4.0

0.75
```

* 파이썬 3 버전의 input과 2.7버전의 raw_input 내장함수는 동일
```
>>> name = raw_input("이름을 입력하세요:")
```

* 소스코드 인코딩 필요
```
# -*- coding: utf-8 -*- 
```

* 에러 처리시 , 로 표기
```
try: 

    4 / 0 

except ZeroDivisionError, e: 

    print e
```
