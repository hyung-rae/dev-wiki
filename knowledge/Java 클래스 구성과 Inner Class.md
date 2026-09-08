---
tags:
  - java
  - class
  - inner-class
  - anonymous-class
---
클래스를 만들 때는 **필드 → 생성자 → 메서드 순서**로 작성한다. 그리고 [[Java 패키지와 클래스 분류|Bean Class와 App Class는 같은 클래스에 섞지 않는다]].

![[java-class-taxonomy.png]]

![[java-class-structure.png]]

## Inner Class
다른 클래스와는 아무 관계를 갖지 않고 ==하나의 클래스와만 관계를 갖는== 클래스. 어디에 선언되느냐에 따라 셋으로 나뉘고, **컴파일된 `.class` 파일 이름이 서로 다르다.**

| 종류 | 위치 | 컴파일 후 이름 |
| --- | --- | --- |
| **member** | 클래스 안의 멤버 | `바깥클래스$안쪽클래스` |
| **Local** | 클래스 안 메서드 내부 | `바깥클래스$1안쪽클래스` |
| **Anonymous** | 이름 없이 선언 | Local과 유사 (안쪽 이름은 공백) |

![[java-inner-class.png]]

## 관련 노트
- [[Java 패키지와 클래스 분류]]
- [[Java 접근 제어자]]
- [[Java super와 this]]
- [[Java]]
