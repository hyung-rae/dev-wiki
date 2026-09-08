---
tags:
  - java
  - interface
  - implements
  - multiple-inheritance
  - abstract
---
Java는 명확한 것을 좋아해서 **다중상속을 지원하지 않고 단일상속만** 지원한다. 그 제약 아래에서 모든 객체를 구현하기 위해 ==`interface`와 `implements`로 보완==한다.

![[java-interface-multiple-inheritance.png]]

## Interface의 성질
- **pure abstract class** — 클래스 안의 **모든 메서드가 abstract**
- 이 인터페이스를 구현하는 클래스는 **오버라이딩을 무조건 해야 한다 (강제성)**
- 인터페이스의 **상태값은 모두 `final static`** 형태다

## abstract와의 차이
| | 오버라이딩 |
| --- | --- |
| **abstract class** | 일부 메서드는 오버라이딩하지 않고 공유 가능 |
| **interface** | **모든** 메서드를 오버라이딩해야 함 |

```java
public class KbBank extends Bank implements Deposit, Payout
// Bank 클래스를 확장하고, Deposit·Payout 인터페이스를 구현한다
```

## interface 기반 프로그래밍
구현체가 아니라 **인터페이스에 의존해 코드를 짜는** 방식.

![[java-interface-programming-1.png]]

![[java-interface-programming-2.png]]

## 관련 노트
- [[Java static final abstract 제어자]]
- [[Java 객체지향의 관계 - 계층화와 일반화]]
- [[Java IO 패키지와 Stream]]
- [[Java]]
