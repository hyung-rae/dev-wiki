---
tags:
  - java
  - package
  - bean-class
  - naming-convention
---
**package는 Java에서 폴더를 관리하는 방법**이다. 클래스가 너무 많아지는 것을 감당하기 위한 계층 구조로, `package a.b`는 ==a 폴더 안에 b가 있다==는 뜻이다.

## 용도에 따른 클래스 구분
| 구분 | 구성 | 역할 |
| --- | --- | --- |
| **Bean Class** | Field, Constructor, Method | 데이터와 동작을 담는 객체 |
| **App Class** | `main` 메서드 | 프로그램 진입점 |

> [!warning]
> Bean Class와 App Class는 **같은 클래스에 작성하지 않는다.** 역할이 다르다.

## 패키지 이름 짓기
오픈소스처럼 전역에서 유일해야 하는 이름은 **도메인 주소를 역순으로** 쓴다 (`com.example.myapp`).

## 관련 노트
- [[Java 플랫폼 독립성과 JVM]]
- [[Java 클래스 구성과 Inner Class]]
- [[Java]]
