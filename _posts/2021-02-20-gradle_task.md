---
{"layout": "post", "categories": "Installation", "title": "gradle task", "feature-img": "assets/img/feature_img.png"}
---
# graddle
명령(gradle compileJava, gradle run)에 의한 task 수행

1. build.graddle 파일에서 task의 처리를 정의해두기
```graddle
task 테스크명 {
    doFist {
        제일 처음에 처리할 내용
    }
    doLast {
        제일 마지막에 처리할 내용
    }

}
```

2. shell에서 실행
```
graddle 테스크명
```

# 매개변수 전달
1. build.graddle에 정의
```graddle
task myTask {
    println("입력한 값은 : "+x)
}
```

2. shell에서 실행
```
gradle myTask -Px=값
```

# 다른 task 호출
```graddle
task 테스크명 {
    doFist{
        println("테스크명의 doFirst 실행..")
        tasks.aaa.execute()
    }
}
task aaa {
    doLast{
        println("aaa의 doLast 실행...")
    }
}
```

# task 종속성 설정
```graddle
task 테스크명 (dependsOn : '선행되어야할task명') {

}
task 테스크명 (dependsOn : ['선행task1','선행task2'] ) {

}
```
