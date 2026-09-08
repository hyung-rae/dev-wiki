---
tags:
  - java
  - super
  - this
  - constructor
  - overriding
---
`super`와 `this`는 **뒤에 괄호가 오느냐 점이 오느냐**로 역할이 완전히 달라진다.

![[java-super-this-override.png]]

## super() / this() — 생성자 호출
**생성자를 호출하는 메서드**이며, 반드시 **생성자의 첫 줄**에 쓴다.

| | 호출 대상 |
| --- | --- |
| `super()` | **상위** 클래스의 생성자 |
| `this()` | **나의** 클래스의 다른 생성자 |

> [!info]
> **모든 생성자 안에는 `super()`가 기본으로 들어가 있다.** 명시하지 않아도 상위 생성자가 먼저 실행된다는 뜻이다.

## super. / this. — Reference
[[Java Reference 형 변환|Reference]]로서 멤버에 접근한다.

| | 가리키는 대상 |
| --- | --- |
| `super.` | 나의 위, **상위** 클래스 |
| `this.` | 나, **지금 내** 클래스 |

```java
super.getA();   // 상위 클래스의 getA()
this.getA();    // 내 클래스의 getA()
```

오버라이딩으로 상위 메서드를 덮었을 때, **덮이기 전 원본에 닿는 통로**가 `super.`다.

## 관련 노트
- [[Java 객체지향의 관계 - 계층화와 일반화]]
- [[Java Reference 형 변환]]
- [[Java 클래스 구성과 Inner Class]]
- [[Java]]
