---
tags:
  - java
  - reference
  - upcasting
  - downcasting
  - polymorphism
---
[[Java 기본형 형 변환|기본형 형 변환]]이 값의 크기 문제였다면, Reference 형 변환은 ==상속 계층에서의 위치== 문제다. 원칙은 하나 — **"작은 개념은 큰 개념에 들어갈 수 있다"** (`~ is a` 관계).

## 묵시적 형 변환 (업캐스팅)
하위 타입을 상위 타입 참조에 담는 것. 자동으로 된다. **서로 다른 하위 타입들을 하나의 배열로 묶어 다룰 수 있다**는 게 실질적 이득이다.

![[java-upcasting.png]]

```java
BusCharge[] bc = new BusCharge[3];
bc[0] = new Student();
bc[1] = new Adult();
bc[2] = new Old();

for (int i = 0; i < bc.length; i++) {
    bc[i].informaint();
    bc[i].charge();     // 각자 오버라이딩한 구현이 실행된다
}
```

## 명시적 형 변환 (다운캐스팅)
상위 타입 참조로는 **하위 클래스에서만 구체화된 메서드에 접근할 수 없다.** 오버라이딩된 메서드는 부르지만, 하위에만 새로 생긴 메서드는 못 부른다.

![[java-downcasting.png]]

```java
s3.a();   // Super의 a(), Sub에서 OverRiding — 접근 가능
s3.b();   // Sub에만 있는 메서드 — 접근 불가
          // "아버지가 나 대신 학원 못 온다"
          // 명시적 형 변환이 필요한 이유
```

> [!warning]
> 다운캐스팅은 **컴파일러를 설득하는 것일 뿐 실제 객체를 바꾸지 않는다.** 실제 타입이 아니면 런타임에 터진다.

## 관련 노트
- [[Java 객체지향의 관계 - 계층화와 일반화]]
- [[Java super와 this]]
- [[Java 기본형 형 변환]]
- [[Java 가비지 컬렉션]]
- [[Java]]
