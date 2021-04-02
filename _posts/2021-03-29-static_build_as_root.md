---
{"layout": "post", "categories": "TroubleShooting", "title": "static build as root", "feature-img": "assets/img/feature_img.png"}
---
# Situation
1. docker volume 으로 연동된 static 디렉토리 : root 소유
2. react 컨테이너는 root가 아닌 container user 권한으로 개발 중

# Solution1 - 명령어로 직접 빌드하기
1. react 도커 컨테이너 접속해 빌드
```
docker exec -it --user root web_frontend_1 /bin/sh
npm run build
```

2. nginx 이미지 재빌드
```
docker-compose up --build -d
```

# Solution2 - 도커 이미지 빌드 시 builder stage 사용
```
FROM node as builder
    ...
RUN npm run build

FROM nginx
    ...
COPY --from=builder /react/build/path /nginx/static/path
```

