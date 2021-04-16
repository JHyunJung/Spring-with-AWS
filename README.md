# Spring-with-AWS

What I learn from here
----------------------

commt - gradle 셋팅

```xml
buildscript 블록 - Gradle 빌드 스크립츠 자체를 위한 의존성이나 변수, Task, Plugin 등을 지정하는 곳이다. 
                  서드파티 플러그인이나 Task, Class 등을 빌드 스크립트 내에서 추가로 사용하려면 해당 의존성을 추가해줘야한다.
        
        ext 블록 - build.gradle에서 사용하는 전역변수 설정
        ex) springBootVersion = '2.1.7.RELEASE'

        repository 블록 - 각종 의존성들을 어떤 원격 저장소에서 받을지 정하는 블록
        dependencies 블록 - 프로젝트 개발에 필요한 의존성들을 선언하는 곳
        
```