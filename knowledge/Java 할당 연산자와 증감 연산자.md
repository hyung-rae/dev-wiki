---
tags:
  - java
  - operator
  - assignment-operator
  - increment-operator
---
**오른쪽 값을 왼쪽 공간에 할당**한다. `=` `+=` `-=` `*=` `/=` `%=` `++` `--`.

> [!warning]
> 두 글자 이상으로 정의된 연산자는 **기호 사이에 공백을 넣으면 안 된다.** `+ =`는 `+=`가 아니다.

```java
int number = 10;
number += 5;   // 15  왼쪽 현재값에 오른쪽을 더한 결과를 다시 왼쪽에
number /= 5;   //  3  나눈 "몫"을 할당
number %= 2;   //  1  나머지를 할당

String str1 = "abc";
str1 += "DEF";  // abcDEF  String도 += 사용 가능
```

## 증감 연산자의 위치
`++` `--`는 값을 1씩 늘리거나 줄인다. ==변수 앞뒤 위치에 따라 그 줄에서의 실행 순서가 달라진다.==

| 형태 | 실행 시점 |
| --- | --- |
| `++number` (전위) | 그 줄에서 **가장 먼저** 실행 |
| `number++` (후위) | 그 줄에서 **가장 나중에** 실행 |

```java
int number = 3;
System.out.println(++number);  // 4  — 먼저 증가하고 출력
System.out.println(number++);  // 4  — 먼저 출력하고 증가
System.out.println(number);    // 5
```

## 관련 노트
- [[Java 산술 연산자]]
- [[Java 비교 연산자와 논리 연산자]]
