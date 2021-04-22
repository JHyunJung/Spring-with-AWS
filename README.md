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
---------------------------------
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
* 자바 개발자들의 필수 라이브러리
* compile('org.projectlombok:lombok') -> build.gradle에 추가
#### @RequiredArgsConstructor
* 선언된 모든 final 필드가 포함된 생성자를 생성해 줍니다.
* final이 없는 필드는 생성자에 포함되지 않습니다.
#### assertj VS Junit
* CoreMatchers와 달리 추가적으로 라이브러리가 필요하지 않다.
* 자동완성이 좀 더 확실하게 지원된다.
* [유튜브](https://www.youtube.com/watch?v=zLx_fI24UXM)
  
Commit - JPA & CRUD API 업데이트
------------------------------
#### JPA
* 관계형 데이터베이스와 객체지향 프로그래밍 언어의 패러다임의 불일치
* 패러다임의 불일치를 중간에서 일치 시켜주기 위한 기술
* SQL에 종속적인 개발을 하지 않아도 된다.
#### Spring Data JPA
* 구현체들을 쉽게 사용하고자 추상화시킨 모듈
* 구현체 교체의 용이성 - Hibernate 외에 다른 구현체로 쉽게 교체
* 저장소 교체의 용이성 - 관계형 데이터베이스 외에 다른 저장소로 쉽게 교체
#### @Entity
* 테이블과 링크될 클래스를 나타냄
* 클래스의 카멜케이스 이름을 언더스코어 네이밍으로 테이블 매칭  
  ex) SalesManager.java -> sales_manager table
#### @Id
* 해당 테이블의 PK 필드를 나타냄
#### @GeneratedValue
* PK의 생성 규칙
* 부트 2.0 이상에서는 GenerationType.IDENTITY 옵션을 추가해야만 auto_increment
#### @Column
* 테이블의 칼럼을 나타내며 굳이 선언하지 않더라도 해당 클래스의 필드는 모두 칼럼이 된다.
* 기본값 외에 추가로 변경이 필요한 옵션이 있으면 사용
* 문자열의 경우 varchar(255)가 기본값인데, 사이즈를 500으로 늘리거나 타입을 변경하고 싶을 경우 사용
#### @NoArgsConstructor
* 기본 생성자 자동 추가
* public Class() {} 와 같음.
#### @Builder
* 해당 클래스의 빌더 패턴 클래스를 생성
* 생성자 상단에 선언 시 생성자에 포함된 필드만 빌더에 포함
#### Spring 웹 계층
* Web Layer
  - 흔히 사용하는 컨트롤러와 뷰 템플릿 영역
  - 외부 요청과 응답에 대한 전반적인 영역
* Service Layer
  - @Service에 사용되는 서비스 영역
  - @Transacional이 사용되어야 하는 영역
* Repository Layer
  - Database와 같이 데이터 저장소에 접근하는 영역
* Dtos
  - 계층 간에 데이터 교환을 위한 객체
* Domain Model
  - 모든 사람이 동일한 관점에서 이해할 수 있고 공유할 수 있도록 단순화시킨 모델
  - 무조건 데이터베이스의 테이블과 관계가 있어야 하는 거는 아님
  
#### Dto 클래스
* Controller와 Service에서 사용
* Entity 클래스를 Request/Response 클래스로 사용하지 않는다.
* Entity 클래스를 기준으로 동작.
* Request와 Response용 Dto는 자주 변경 필요한 클래스
* View Layer와 DB Layer 역할 분리

#### @SpringBootTest
* @WebMvcTest의 경우 JPA기능이 작동하지 않는다.
* JPA 기능까지 한번에 테스트할 때는 @SpringBootTest 사용

#### JPA CRUD
update 기능에서 DB에 쿼리를 날리지 않는다. Cuz JPA의 영속성 컨텐스트 때문에  
영속석 컨텍스트란, 엔티티를 영구 저장하는 환경으로 JPA의 핵심 내용은 엔티티가 영속성 컨텍스트에 포함되어 있느냐 이다.  
트랜잭션 안에서 DB에서 데이터를 가져오면 데이터는 영속성 컨텍스트가 유지된 상태이다.  
해당 데이터의 값을 변경하면 트랜잭션이 끝나는 시점에 해당 테이블에 변경분을 반영한다 -> Update 쿼리를 날릴 필요가 없다.  
[더티 체킹](https://jojoldu.tistory.com/415)

#### @MappedSuperclass
* JPA Entity 클래스들이 BaseTimeEntity을 상속할 경우 필드들도 칼럼으로 인식하도록 한다.

#### @EntityListeners(AuditingEntityListener.class)
* BaseTimeEntity 클래스에 Auditing 기능을 포함시킨다.ㄲ

Commit - Posts CRUD & Mustache View 업데이트
------------------------------------------
#### 템플릿 엔진이란?
지정된 템플릿 양식과 데이터가 합쳐져 HTML문서를 출력하는 SW    
ex)
* 서버 템플릿 엔진 - JSP, Freemarker
* 클라이언트 템플릿 엔진 - React, Vue

##### 서버 템플릿 엔진
서버에서 구동, 서버에서 Java 코드로 문자열을 만든 뒤 이 문자열을 HTML로 변환하여 브라우저로 전달
##### 클라이언트 템플릿 엔진
브라우저 위에서 작동, 브라우저에서 화면을 생성, 서버에서 이미 코드가 벗어남, 클라이언트에서 조립

#### Mustache
대부분 언어를 지원하는 심플한 템플릿 엔진  
장점
* 문법이 다른 템플릿 엔진보다 심플
* 로직 코드를 사용할 수 없어 View의 역할과 서버의 역할이 명확하게 분리
* Mustache.js와 Mustache.java 2가지가 다 있어, 하나의 문법으로 클라이언트/서버 템플릿을 모두 사용 가능

#### Return "view file name"
* 컨트롤러에서 문자열을 반환할 때 앞의 경로와 뒤의 파일 확장자는 자동으로 지

#### 부트스트랩
* 외부 CDN을 사용
  * 단점 - CDN에서 문제가 생기면 덩달아 같이 문제가 생길 수 있다.
  
* 직접 라이브러리를 받아서 사용

#### CSS와 JS 위치
HTML은 위에서부터 코드가 실행되기 때문에 head가 다 실행되고서야 body가 실행  
즉, head가 다 불러지지 않으면 사용자 쪽에선 백지 화면만 노출,특히 js의 용량이 크면 클수록 body 부분의 실핼이 늦어지기 때문에 js는 body 하단에 두어 화면이 다 그려진 뒤에 호출하는 것이 좋다.  
반면, css는 화면을 그리는 역할이므로 head에서 불러오는 것이 좋다. 그렇지 않으면 css가 적용되지 않은 깨진 화면을 사용자가 볼 수 있기 때문이다.

#### Querydls 추천 이유
* 타입 안정성이 보장
* 국내 많은 회사에서 사용 중
* 레퍼런스가 많음