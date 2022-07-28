# Spring-Template-Project
Spring Template Project

## 스프링과 표준프레임워크

표준프레임워크는 스프링 프레임워크을 기반으로 만들어졌다.   
스프링 프레임워크가 등장하기 이전에 자바 기반의 엔터프라이즈 애플리케이션은 대부분 EJB(Enterprise Java Beans)로 개발했었다.   
하지만 EJB는 EJB 컨테이너가 제공하는 많은 기능과 나름의 장점에도 불구하고 외면받았다.   
그 이유는 이 컴포넌트를 배치하고 실행하려면 고가의 장비인 WAS가 필요하다.   
따라서 평범한 POJO(Plain Old Java Object)를 이용한 스프링 프레임워크를 학습하고자 한다.   
POJO란 말그대로 평범한 옛날 자바 객체를 의미하며 이미 많은 디자인 패턴이 적용되어 배포되므로 프레임워크를 사용하는 것 자체가 디자인 패턴을 사용하는 것이다.   

## 스프링 프레임워크의 특징

1. 경량 : 스프링은 여러 개의 모듈로 구성되어 있으며, 각 모듈은 하나 이상의 JAR 파일로 구성된다. 이 몇 개의 JAR 파일만 있으면 개발과 실행이 모두 가능하며 크기 역시 몇 메가바이트를 넘지 않는다. 

2. 제어의 역행 IoC (Inversion of Control)
비즈니스 컴포넌트를 개발할 때, 항상 신경 써야하는 것이 낮은 결합도와 높은 응집도이다. 스프링은 제어의 역행을 통해 낮은 결합도를 유지한다.

3. 관점지향(Aspect Oriented Programming, AOP)
관점지향 프로그래밍은 비즈니스 메소드를 개발할 때, 핵심 비즈니스 로직과 각 비즈니스 메소드마다 반복해서 등장하는 공통 로직을 분리해서 응집도가 높게 개발할 수 있도록 지원한다.

4. 컨테이너(Container)
컨테이너는 특정 객체의 생성과 관리를 담당하며 객체 운용에 필요한 다양한 기능을 제공한다. 대표적으로 Servlet 컨테이너와 EJB 컨테이너가 있다.

## 표준프레임워크 템플릿 프로젝트

템플릿 프로젝트를 만들고 표준프레임워크가 제공하는 템플릿 소스의 구조를 분석하고자 한다.   
표준프레임워크로 웹 프로젝트를 생성하기 위해서는 File -> New -> eGovFrame Web Project 메뉴를 선택한다.   
![image](https://user-images.githubusercontent.com/58906858/181198501-d399501b-81f0-46fd-b7c0-63aa76339ea2.png)

Next를 누르면 예제 소스를 생성하는 화면이 나온다. 여기서 Generate Example이라는 체크박스를 체크하고 Finish를 클릭하면 예제 소스가 포함된 템플릿 프로젝트가 생성된다.   
![image](https://user-images.githubusercontent.com/58906858/181198659-dce5c137-7f33-454b-ba72-d1f59f094f9a.png)

## 웹 프로젝트 실행

표준프레임워크를 통해 생성된 웹 프로젝트에는 템플릿 소스가 들어잇으며, 자바로 만든 HSQLDB라는 데이터베이스도 가지고 있기 때문에 독립적으로 실행할 수 있다.   
프로젝트 오른쪽 마우스 클릭 후 Run As -> Run on Sever를 선택한다.   
다음과 같이 서버가 구동되어 브라우저에 샘플 목록화면이 출력된다.   
![image](https://user-images.githubusercontent.com/58906858/181200298-a3453d0b-5050-405a-bab9-413613f38555.png)

중요한 것은 프로젝트가 실행될 때, sampledb.sql 파일에 있는 SQL이 실행되어 데이터베이스에 SAMPLE 테이블이 자동으로 생성되고 입력된다는 것이다.   
목록화면에서 카테고리ID를 클릭하면 상세화면으로 이동한다.   
![image](https://user-images.githubusercontent.com/58906858/181201412-f907b011-86b9-47b1-b48f-e60ebc09a314.png)

상세화면에는 목록, 수정, 삭제, 재설정 버튼이 있어서 수정이나 삭제를 요청할 수 있다.   
그리고 템플릿 프로젝트에서 사용하는 SAMPLE 테이블은 메모리 테이블로 생성되기 때문에 톰캣 서버를 재구동하면 테이블도 다시 생성되고 데이터도 다시 저장된다.   

## 표준프레임워크 템플릿 프로젝트 구조 분석

### 프레임워크 라이브러리
표준프레임워크가 제공하는 템플릿 프로젝트에서 가장 먼저 확인할 것은 Maven Dependencies인데 이곳에 프로젝트 수행에 필요한 온갖 라이브러리들이 들어있기 때문이다.   
![image](https://user-images.githubusercontent.com/58906858/181411063-ed1da0ba-9aea-484e-bccd-5f11532d97c8.png)

다운로드된 라이브러리들은 의존 관계로 얽혀있는데 각 라이브러리들의 의존관계를 확인하려면 pom.xml파일을 오픈해서 파일의 탭중에서 Dependency Hierarchy 탭을 클릭해서 확인할 수 있다.   
![image](https://user-images.githubusercontent.com/58906858/181411232-07c231d3-97a9-4c9c-a9d9-be39965e5093.png)

### src/main/java 소스 폴더

src/main/java 소스 폴더는 프로젝트의 자바 소스들이 들어있는 폴더로서 크게 비즈니스 컴포넌트와 웹 컴포넌트 패키지로 구성되어 있다.   
![image](https://user-images.githubusercontent.com/58906858/181411667-6d6ec92b-672b-4954-9273-f50b7076f921.png)

1. egovframework.example.sample.service : 이 패키지에는 비즈니스 컴포넌트가 클라이언트에 공개할 인터페이스와 VO 클래스들이 들어있다.
2. egovframework.example.sample.service.impl : 이 패키지에는 비즈니스 컴포넌트의 구현클래스에 해당하는 클래스가 들어있다.
3. egovframework.example.sample.web : 이 패키지에는 웹 컴포넌트에 해당하는 컨트롤러 클래스가 들어있다.

### src/main/resources 소스 폴더

src/main/resources 소스 폴더에는 XML 파일을 비롯하여 프레임워크에서 사용할 다양한 설정 파일들이 들어있다.   
표준프레임워크는 크게 3개의 오픈소스 프레임워크(Spring, iBATIS, MyBatis)를 사용한다.   
![image](https://user-images.githubusercontent.com/58906858/181412200-c5751a37-16ab-422f-a003-6217b149d5d1.png)

1. db폴더 : 테이블 생성 및 테스트 데이터 관련 SQL 파일이 있다.
2. egovframework/message : 다국어와 관련한 메시지 파일들이 있다.
3. egovframework/spring : 스프링 프레임워크와 관련된 모든 XML 파일들이 있다. 스프링 설정 파일은 기능별로(트랜잭션, 데이터 소스, iBATIS/MyBatis 연동, AOP 연동 등) 나누어서 관리한다.
4. egovframework/sqlmap : iBATIS, MyBatis 연동과 관련된 메인 설정 파일들과 SQL 파일들이 등록되어 있다.
5. log4j2.xml : 프로젝트 실행 과정에서 생성되는 다양한 로그를 관리한다.

### src/main/webapp 폴더

src/main/webapp 폴더는 앞에서 살펴본 src/main/java, src/main/resources 같은 소스 폴더가 아닌 단순 일반 폴더이다.   
복잡한 웹관련 리소스들이 등록되어 관리된다.   
![image](https://user-images.githubusercontent.com/58906858/181412916-1495d991-a5e9-437b-a133-653862d97688.png)

1. css : 디자인 관련한 스타일 시트
2. images : 디자인 관련한 이미지 폴더
3. index : 메인 화면이자 웰컴 파일에 해당하는 인덱스(index.jsp)파일
4. WEB-INF : 웹 프로그램의 배치 기술 문서(web.xml), spring 설정 파일, JSP 파일   
5. WEB-INF/config : springmvc 폴더에는 스프링컨테이너가 로딩할 환경설정 파일인 dispatcher-servlet.xml 파일에 스프링 MVC와 관련한 설정들이 포함되어있다.   
VALIDATOR 폴더에는 유효성 체크와 관련한 XML 파일이 들어있는데 이 파일을 이용하면 사용자가 입력한 데이터가 비즈니스 컴포넌트로 전달되기 전에 한번 더 체크할 수 있다.   
![image](https://user-images.githubusercontent.com/58906858/181413230-38225b46-b6bd-4bdd-b536-04e7471fb8b2.png)
6. WEB-INF/jsp : 템플릿 프로그램에서 화면으로 사용할 여러 JSP 파일들이 들어있다.   
1. egovframework/exmaple.cmm : 예외 처리 관련 JSP 파일
2. egovframework/example/sample : 예제 목록 화면과 등록/상세 화면 관련 JSP 파일   
![image](https://user-images.githubusercontent.com/58906858/181413508-46e906c3-be7d-4ccb-a6bc-dce680f871aa.png)

## 이후 스프링 학습 계획

표준프레임워크가 제공하는 복잡한 템플릿 프로젝트의 구조를 살펴보았다. 이후에는 템플릿 프로젝트가 제공하는 소스들을 직접 만들어보면서 표준프레임워크의 문법을 이해하고 적용한다. 표준프레임워크 문법 = 스프링 문법
