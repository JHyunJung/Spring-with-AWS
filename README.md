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

Commit - Controller & Test 업데이트
-------------------
#### TDD의 장점
* 빠른 피드백
* 자동검증
* 기존 기능 보호
* JUnit - java, DBUnit - DB
#### @SpringBootApplication
스프링 부트의 자동 설정, 스프링 Bean 읽기와 생성을 모두 자동으로 설정, @이 있는 위치부터 설정을 읽어가기 떄문에
항상 프로젝트의 최상단에 위치해야 한다.
#### @RestController
컨트롤러를 JSON을 반환하는 컨트롤러로 만들어 준다.
#### @RunWith(SpringRunner.class)
* 테스트를 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자를 실행
* 스프링 부트 테스트와 JUnit 사이에 연결자 역할을 한다.
#### @WebMvcTest
* Web에 집중할 수 있는 어노테이션
* Controller, @ControllerAdvice등을 사용 가능, @Service, @Component, @Repository 사용 X
#### @AutoWired
* 스프링 관리하는 Bean을 주입
#### private MOckMvc mvc
* 웹 API 테스트할 때 사용
#### mvc.perform(get("/hello")) 
* MockMvc를 통해 /hello 주소로 HTTP GET 요청
#### lombok
* 자바 개발자들의 필수 라이브러
* compile('org.projectlombok:lombok') -> build.gradle에 추가
#### @RequiredArgsConstructor
* 선언된 모든 final 필드가 포함된 생성자를 생성해 줍니다.
* final이 없는 필드는 생성자에 포함되지 않습니다.
#### assertj VS Junit
* CoreMatchers와 달리 추가적으로 라이브러리가 필요하지 않다.
* 자동완성이 좀 더 확실하게 지원된다.
* [유튜브](https://www.youtube.com/watch?v=zLx_fI24UXM)