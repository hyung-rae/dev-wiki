---
tags:
  - java
  - wrapper-class
  - autoboxing
  - primitive-type
---
`equals()` 같은 메서드는 **객체끼리만 비교**할 수 있어서 **primitive type 8개는 인자로 들어갈 수 없다.** 이 간극을 메우는 것이 ==Wrapper Class==다 — primitive 값을 객체로 감싼다.

```java
int i;
double d;

Integer boxed = new Integer(i);
Double  boxedD = new Double(d);
// wrapper class를 활용해 data type 변경
```

## AutoBoxing / UnBoxing
JDK 1.5부터는 그 변환을 **컴파일러가 대신 해준다.** Wrapper Class를 더 쉽게 쓰기 위한 문법 설탕이다.

```java
// jdk 1.4 — 직접 감싸야 했다
Integer i = new Integer(intValue);
Double  d = new Double(doubleValue);
Boolean b = new Boolean(boo);

// jdk 1.5 — 대입만 하면 된다
Integer i = intValue;      // AutoBoxing
Double  d = doubleValue;
Boolean b = boo;
```

반대로 `Integer`를 `int` 자리에 넣는 것이 **UnBoxing**이다.

## 관련 노트
- [[Java 배열과 Vector]]
- [[Java 기본형 형 변환]]
- [[Java]]
