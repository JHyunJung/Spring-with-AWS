# Spring-with-AWS

What I learn from here
======================

Commit - Gradle 셋팅
-------------------

#### buildscript 블록
Gradle 빌드 스크립트 자체를 위한 의존성이나 변수, Task, Plugin 등을 지정하는 곳이다. 
서드파티 플러그인이나 Task, Class 등을 빌드 스크립트 내에서 추가로 사용하려면 해당 의존성을 추가해줘야한다.

##### ext 블록
build.gradle에서 사용하는 전역변수 설정
ex) springBootVersion = '2.1.7.RELEASE'

#### 'apply plugin:'
Gradle 플러그인을 사용하기 위한 것
* apply plugin: 'org.springframework.boot'
* apply plugin: 'io.spring.dependency-management'

#### repository 블록
각종 의존성들을 어떤 원격 저장소에서 받을지 정하는 블록
* mavenCentral() - Apache Maven 중앙 저장소
* jcenter() - JCenter라는 저장소

#### dependencies 블록 - 저장소에서 필요한 라이브러리를 사용하는데 사용할 수 있는 것
* compile('org.springframework.boot:spring-boot-starter-web') - 컴파일시에 사용하는 라이브러리
* testCompile('org.springframework.boot:spring-boot-starter-test') - 테스트 컴파일에 사용하는 라이브러리
        
