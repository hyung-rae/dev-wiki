---
tags:
  - java
  - control-statement
  - loop
  - for-loop
  - while-loop
---
조건식을 체크해 true면 코드를 실행하고, **실행 후 조건식을 다시 체크**해 true면 또 실행한다. false가 나오면 종료.

| | 쓰는 상황 |
| --- | --- |
| **`for`** | 반복 횟수가 비교적 **명확할 때** |
| **`while`** | 특정 **조건을 만족하는 동안** 계속 |

## while
`if`와 형태가 거의 같다. 차이는 "한 번 실행"이 아니라 "조건이 참인 동안 반복"이라는 점.

```java
int num = 4;
while (num > 0) {
    System.out.println("num : " + num);
    num--;              // 이게 없으면 무한 루프
}
```

## for
세 부분을 세미콜론으로 나눠 **제어 변수의 생애 전체**를 한 줄에 적는다.

```java
// for (초기화식 ; 반복 조건식 ; 변화식)
for (int i = 0; i < 3; i++) {
    System.out.println(i);
}

// 초기화식·조건식에 다른 변수도 쓸 수 있다
int start = 1, end = 4;
for (int i = start; i <= end; i++) { ... }
```

## 관련 노트
- [[Java 조건문]]
- [[Java 코드 블록과 변수 유효범위]]
- [[Java 배열과 Vector]]
- [[Java]]
