---
tags:
  - java
  - thread
  - synchronized
  - deadlock
  - concurrency
---
프로세스는 **고자원**이고, 프로세스끼리 data를 교환하려면 [[Java IO 패키지와 Stream|io]]가 필요하다. 그래서 ==하나의 프로세스 안에서 여러 작업을 실행하는 것==이 효율적이다 — Multi-Thread, Multi-tasking.

![[java-thread-multitasking-1.png]]

![[java-thread-multitasking-2.png]]

## start()를 갖는 두 가지 방법
1. **`Runnable` interface implements** — Thread 생성자에는 Runnable 타입만 들어간다. Runnable을 구현해 Thread 생성자에 넘긴 뒤 `start()` 접근
2. **Thread가 되기** — `Thread` 클래스를 extends한 뒤 `start()` 접근

## 우선순위
```java
setPriority();   // static final

Thread.MAX_PRIORITY;
Thread.NORM_PRIORITY;
Thread.MIN_PRIORITY;
```

## Life Cycle
![[java-thread-lifecycle.png]]

## 동기화 문제
스레드는 data를 공유해 효율적이지만, **하나의 data를 여럿이 공유하면 신뢰성이 떨어진다.**

![[java-thread-sync-problem.png]]

## Synchronized — "key를 갖고 들어가라"
한 번에 하나의 스레드만 들어가도록 잠근다. 나머지는 Synchronized Pool에서 대기한다.

![[java-synchronized.png]]

> [!tip]
> 메서드 전체가 아니라 **`Synchronized` 블록으로 필요한 곳에만** 거는 것이 효율적이다. 스레드가 **Synchronized Pool에 머무는 시간이 줄어든다.**

## Dead Lock
key를 가진 스레드가 계속 실행되어 **다른 스레드가 Synchronized Pool에서 영영 나오지 못하는** 상태.

![[java-deadlock.png]]

## 관련 노트
- [[Java IO 패키지와 Stream]]
- [[Java Interface와 다중상속 보완]]
