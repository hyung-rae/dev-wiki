---
tags:
  - java
  - operator
  - comparison-operator
  - logical-operator
  - boolean
---
두 연산자는 짝으로 쓰인다. **비교 연산자가 `boolean`을 만들고, 논리 연산자가 그 `boolean`들을 조합**한다.

## 비교 연산자
왼쪽과 오른쪽을 비교해 `true` / `false`를 낸다. `<` `<=` `>` `>=` `==` `!=`

- `==` : 두 값이 **같으면** true
- `!=` : 두 값이 **다르면** true

## 논리 연산자
| 연산자 | 이름 | 결과가 true인 조건 |
| --- | --- | --- |
| `&&` | AND | **양쪽 모두** true |
| `\|\|` | OR | **하나라도** true |
| `!` | NOT | 원래 값이 false (해당 줄에서만 뒤집음) |

```java
boolean b = true;
System.out.println(!b);  // false
System.out.println(b);   // true — 원본은 바뀌지 않는다
```

> [!tip]
> 논리 연산자를 `true`/`false` 리터럴에 직접 쓰는 일은 드물다. 대부분 **`boolean`을 결과로 내는 비교 연산자나 메서드**를 묶는 데 쓴다 — `if (age >= 19 && hasTicket())`.

## 관련 노트
- [[Java 조건문]]
- [[Java 산술 연산자]]
- [[Java 할당 연산자와 증감 연산자]]
