---
{"layout": "post", "categories": "Installation", "title": "eclipse debugging", "feature-img": "assets/img/feature_img.png"}
---
﻿## 디버깅
1. break point(중단점) 만들기 : 원하는 지점의 줄번호 옆을 마우스 클릭
2. F11을 눌러 디버깅모드로 시작하면 디버깅 창이 뜬다.
3. 디버깅 창에서 아이콘을 선택하거나, 단축키를 눌러 기능 수행
- Ctrl+Alt+B : 모든 중단점 건너뛰기
- F5 : 1단계 프로세스 진행-함수 안으로 들어감
- F6 : 1단계 프로세스 진행-함수 안으로 안 들어감
- F7 : 함수의 리턴값만 확인하고 호출부로 돌아감
- F8 : 다음 중단점까지 쭉 진행
- Drop to Frame : 현재 단계의 스택 프레임 첫행으로 이동(다시 시작)
4. 디버깅 진행 중 변수에 커서를 위치하면 변수 값 확인 가능
5. 또는 Variables 창에서 모든 변수의 값 확인 가능
6. 또는 Expressions 창에서 사용자가 추가한 변수만 관리 가능
- 변수 추가 방법 : 변수를 오른쪽 클릭 > Watch

## 디컴파일러 설치(이클립스)
다음 사이트에서 jd-...-.zip 파일 다운로드
```
http://jd.benow.ca/
```
이클립스 메뉴에서
```
Help - Install new software - addrepository - archive
```
설치 후 F3을 누르면 .class 파일의 소스코드를 볼 수 있음









