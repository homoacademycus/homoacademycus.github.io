---
{"layout": "post", "categories": "TroubleShooting", "title": "jekyll chirpy", "feature-img": "assets/img/feature_img.png"}
---
# 수정할 점
- 검색창 엔터 동작 안함
- 페이지네이션 ul 점으로 뜸
- 탭 아래에 스크롤바 생기며 블로그 타이틀이 overflow 시 hidden 됨
- 탭 메뉴에 카테고리 메뉴를 클릭해서 들어가야 카테고리가 보임

# 초기화
```
chmod -R a+w /srv/jekyll
bundle (online 상태에서)
bash tools/init.sh --no-gh
```
--no-gh 옵션: .github 디렉토리와 중국어 docs, default posts 삭제

# _config.yaml
```
lang: en-US
timezone: Asia/Seoul
img_cdn: '/images' #로컬, CORS 자원 가능 'https://cdn.com'
avatar: /avatar.png #아바타 이미지
theme_mode: dark
paginate: 5
toc: true #목차
disqus: #댓글
  comments: false
  shortname: ''
social: #하단의 footer에 보여질 소유자 정보
  name: homoacademycus
  email: homoacadmycus@github.com
  links: #첫째 요소가 소유자의 링크로 쓰인다
    - https://github.com/homoacademycus  
    - https://twitter.com/homoacademycus
google_site_verification: google_meta_tag_verification_string    
exclude:
  - '*.git*'
jekyll-archives:
  enabled: [categories, tags]
  layouts:
    category: category
    tag: tag
  permalinks:
    tag: /tags/:name/
    category: /categories/:name/
```

# 포스트 수준 설정 - 기본
```
title: 포스트제목
categories: [1차카테고리, 2차카테고리]
tags: [태그명] #소문자여야
image: #포스트의 맨 위에 이미지 추가
  src: /path/to/image/file
  alt: 대체문자
```

# 포스트 수준 설정 -  글로벌 설정 오버라이드
```
toc: false #포스트 우측에 보여지는 목차
comments: false #댓글
math: true #성능을 위해 default로 로딩 안하는 기능이라
mermaid: true #다이어그램 생성툴
```

# assets/img/favicons 커스터마이징
```
https://www.favicon-generator.org/
```
