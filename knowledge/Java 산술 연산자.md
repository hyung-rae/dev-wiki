---
tags:
  - java
  - operator
  - arithmetic-operator
  - string-concatenation
---
사칙연산과 나머지, **`+` `-` `*` `/` `%` 5개**로 이루어진다. 핵심 규칙 두 가지가 결과 타입을 결정한다.

- **서로 다른 타입을 연산하면 결과는 둘 중 더 큰 타입**이 된다 (정수 + 실수 = 실수)
- **정수 ÷ 정수는 몫만 남는다** — 소수점은 버려진다

```java
int number = 3, number2 = 7;
number / number2   // 0    (3/7의 몫)
number % number2   // 3    (나머지)

double d2 = 7.0;
number / d2        // 0.42857...  정수+실수 → 실수
```

## `+`의 예외: String
String에 `+`를 쓰면 **연산이 아니라 이어붙이기**가 된다. 다른 타입이 섞이면 **먼저 String으로 변환한 뒤** 연결한다.

```java
System.out.println("100" + 100);  // 100100
System.out.println(100 + 100);    // 200
```

## 관련 노트
- [[Java 기본형 형 변환]]
- [[Java 할당 연산자와 증감 연산자]]
- [[Java 비교 연산자와 논리 연산자]]
