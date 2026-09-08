---
tags:
  - java
  - control-statement
  - conditional-statement
  - switch
---
==조건식이 true일 때 해당 코드 블록을 실행==하는 제어문. Java에는 `if` 계열과 `switch` 두 갈래가 있다.

## if / if-else / else if
`if`가 false면 `else` 블록이, true면 `if` 블록이 **무조건** 실행된다. 다른 조건식으로 더 갈라야 하면 `else if`를 쓴다.

```java
if (num == 1) {
    System.out.println(1);
} else if (num == 2) {
    System.out.println(2);
} else {
    System.out.println("그 외의 수");
}
```

> [!warning]
> `else if`는 원하는 만큼 넣을 수 있지만 **`else`가 나온 이후에는 쓸 수 없다.** `else`가 사슬의 끝이다.

## switch
**하나의 정수형 또는 String 변수**를 놓고 가능한 값별로 실행할 코드를 나열한다.

```java
switch (num) {
case 1:
    System.out.println("num = 1");
    break;
case 3:
    System.out.println("num = 3");
    break;
default:
    System.out.println(num);
    break;
}
```

> [!warning]
> `break`가 없으면 **다음 `break`를 만날 때까지 아래 case들이 모두 실행된다**(fall-through). 의도한 게 아니라면 각 case마다 반드시 넣는다.

## 관련 노트
- [[Java 반복문]]
- [[Java 코드 블록과 변수 유효범위]]
- [[Java 비교 연산자와 논리 연산자]]
