---
tags:
  - java
  - exception
  - try-catch
  - throw
  - troubleshooting
---
==Exception은 프로그램 코드로 수습될 수 있는 미약한 오류==다. 예외 처리의 목적은 **견고한 앱을 만드는 것**, 곧 **프로그램을 끝까지 정상 종료시키는 것**이다.

![[java-exception-concept.png]]

## Exception 계층
`catch()` 안에는 **Throwable 하위만** 올 수 있다.

![[java-exception-hierarchy.png]]

## try - catch
```java
try {
    // 예외가 발생할 가능성이 있는 코드

} catch (Exception1 e1) {
    // 다중 catch는 계층의 "하위"부터 작성해야 한다 (아니면 컴파일 에러)

} catch (Exception e) {
    e.printStackTrace();
    // Exception은 stack 형식으로 출력되므로
    // 문제와 가장 가까운 코드를 찾기 쉽게 꼭 작성한다
}
```

> [!warning]
> **다중 `catch`는 하위 예외부터 적는다.** 상위(`Exception`)를 먼저 적으면 아래 catch에 절대 닿지 못해 에러가 난다. 혹시 모를 경우를 대비해 **마지막 catch에 최상위 `Exception`**을 두는 것이 안전하다.

## finally
`finally` 블록은 ==예외 발생 여부와 무관하게 반드시 실행==된다. 자원 반납처럼 빠뜨리면 안 되는 코드를 넣는다.

## throws — 예외 위임
예외를 처리하지 않고 **발생 근원지 코드로 던진다.** 근본적인 해결책은 아니다.

## 사용자 정의 Exception
Java가 주는 것 말고 나만의 예외가 필요할 때가 있다. **`Exception` 클래스는 extends가 가능**하다.

> [!info]
> 직접 만든 예외는 **JVM이 발생시켜 주지 않는다.** `throw` 키워드로 **직접 발생시켜야** 한다.

## 관련 노트
- [[Java static final abstract 제어자]]
- [[Java IO 패키지와 Stream]]
