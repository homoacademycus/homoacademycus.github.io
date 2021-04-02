---
{"layout": "post", "categories": "TroubleShooting", "title": "nginx proxy django 502", "feature-img": "assets/img/feature_img.png"}
---
# symtom
```
client <-http-> nginx(proxy) <-http-> was
```

# possible cause and solution -1
nginx and django communicate with WSGI protocol, not HTTP protocol
```
upstream server가 nginx의 socket 생성 자체를 해주지 못해서
```
- in response header
```

```
- setup a WSGI HTTP server
```

```

# possible cause and solution - 2
HTTP 프로토콜 timeout - API 측에 cluster 설정이 없는 경우
```
nginx proxy_timeout 10sec
tomcat connectionTimeout 5sec
```
upstream 에서 Fin 전송(끊기위해) 후 RST를 전송하기 전에 새로운 요청이 들어옴
```
proxy_timeout (nginx proxy, AJP...etc)  < upstream timeout
```
- 모든 요청은 KeepAlive로 upstream으로 전달 되도록 구성되어야
- 별도의 프로토콜 stack을 구성하면 이런 문제가 발생 안함(장고의 wsgi, 톰캣의 ajp ...)
```
http 요청이 web 으로 들어오면 AJP protocol로 wraping 되어 tomcat의 별도 AJP Port로 통신
```

# possible cause and solution -3
if need more header size, configure buffer size(느리거나 용량문제로 발생하는 504와 다름)
```
proxy_buffering on;
proxy_buffers 64 4k;
proxy_buffer_size 128k;
```

# possible cause and solution -4
due to server's problem, not network problem?


