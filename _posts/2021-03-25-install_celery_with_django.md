---
{"layout": "post", "categories": "Installation", "title": "install celery with django", "feature-img": "assets/img/feature_img.png"}
---
# 설정 - djangoProj/configs/settings.py

```
CELERY_BROKER_URL='amqp://rabbitmq:6379'
CELERY_RESULT_BACKEND='django-db'
CELERY_RESULT_SERIALIZER = 'json'
CELERY_TASK_SERIALIZER = 'json'
CELERY_TIMEZONE = 'Asia/Seoul'
CELERY_ACCEPT_CONTENT = ['application/json']
```

- 문자열을 사용하여 worker가 자식 프로세스로 설정객체를 serialize하지 않아도 되도록

# 실행 명령어

```
celery --app=configs worker --loglevel=info
```

# 벡엔드 : 작업 결과 기록 - django

- django의 ORM 또는 cache 프레임워크 사용가능한 모듈

```
pip3 install django-celery-results
pip3 install django-celery-beat
```

- settings.py 등록

```
INSTALLED_APPS = (
    'django_celery_results',
)
CELERY_RESULT_BACKEND = 'django-db'
 #CELERY_CACHE_BACKEND = 'django-cache'
```

- celery가 사용할 데이터베이스 생성

```
python3 manage.py migrate django_celery_results
```

