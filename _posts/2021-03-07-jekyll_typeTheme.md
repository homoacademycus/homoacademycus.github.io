---
{"layout": "post", "categories": "TroubleShooting", "title": "jekyll typeTheme", "feature-img": "assets/img/feature_img.png"}
---
# 초기화
```
chmod -R a+w /srv/jekyll
bundle install
jekyll build
jekyll serve
```

# _config.yaml
```
search: true
```

# 포스팅 - 기본
```
layout: post
title: 포스트제목
feature-img: "assets/img/sample_feature_img.png"
feature-title: 이미지제목
tags: [태그1, 태그2]
```

# 포스팅 - 추가
```
hide: true #네비게이션바에서 안보이게
order: 4 #네비게이션바에서 정렬 순서
subtitle: "부제목"
permalink: /404.html
```


