---
tags:
  - java
  - moc
---
Java 학습 노트의 목차. 아래로 갈수록 앞의 개념을 전제로 한다.

## 기초
- [[Java 플랫폼 독립성과 JVM]] — 바이트코드와 WORA, 그 대가인 실행 속도
- [[Java 패키지와 클래스 분류]] — package의 폴더 관리, Bean/App Class
- [[Java 기본형 형 변환]] — 암시적·명시적 기준, 오버플로우

## 연산자
- [[Java 산술 연산자]] — 결과 타입 결정 규칙, String의 `+`
- [[Java 할당 연산자와 증감 연산자]] — 전위·후위 실행 순서
- [[Java 비교 연산자와 논리 연산자]] — boolean을 만들고 조합하기

## 제어문
- [[Java 조건문]] — if / else if / switch
- [[Java 반복문]] — for와 while의 선택 기준
- [[Java 코드 블록과 변수 유효범위]] — `{}`가 변수의 수명을 정한다

## 입출력
- [[Java 콘솔 출력 - print println printf]] — printf 서식 문자
- [[Java Scanner와 버퍼 메모리]] — `nextLine()`이 빈 값을 주는 이유

## 객체지향
- [[Java 클래스 구성과 Inner Class]] — 작성 순서와 Inner Class 3종
- [[Java 접근 제어자]] — 캡슐화, private 생성자
- [[Java static final abstract 제어자]] — Object Modeling에서의 의미
- [[Java 객체지향의 관계 - 계층화와 일반화]] — `is a` 관계의 성립
- [[Java super와 this]] — 괄호(생성자)와 점(Reference)의 차이
- [[Java Reference 형 변환]] — 업캐스팅의 이점, 다운캐스팅이 필요한 이유
- [[Java Interface와 다중상속 보완]] — 단일상속 제약을 메우는 방법

## 자료 구조
- [[Java 배열과 Vector]] — 타입·크기 제약의 차이, Generic
- [[Java Wrapper Class와 오토박싱]] — primitive를 객체로 감싸기

## 런타임과 심화
- [[Java 가비지 컬렉션]] — Reference Count로 판정하는 수거 기준
- [[Java 예외 처리]] — 다중 catch 순서, finally, 사용자 정의 예외
- [[Java IO 패키지와 Stream]] — SinkStream/FilterStream, Marker Interface
- [[Java Thread와 동기화]] — Synchronized와 Dead Lock

## 데이터베이스 연동
- [[JDBC]] — Connection → Statement → ResultSet

## 함께 보기
- [[시스템 개발 절차 - 모델링과 프로그래밍]] — 코딩 전에 결정하는 것들
