---
tags:
  - java
  - jvm
  - bytecode
  - platform-independence
---
Java는 ==OS에 독립적인 플랫폼==이다. 소스를 OS별 기계어가 아니라 **바이트코드(`.class`)로 컴파일**하고, 각 OS에 맞는 **JVM이 이를 해석해 실행**한다. "한 번 작성하면 어디서든 실행(WORA)"의 근거다.

![[java-platform-independence.png]]

## 대가: 실행 속도
JVM이라는 해석 계층이 하나 더 끼기 때문에, **네이티브 컴파일 언어보다 실행이 느리다.** 독립성과 속도를 맞바꾼 구조다.

![[java-jvm-execution-speed.png]]

> [!info]
> Java의 다른 성격들 — 객체지향 언어(OOPL), 에디터에 독립적인 개발, 분산환경 적합성 — 도 이 "표준 런타임 위에서 돈다"는 전제에서 나온다.

## 관련 노트
- [[Java 패키지와 클래스 분류]]
- [[Java 가비지 컬렉션]]
- [[시스템 개발 절차 - 모델링과 프로그래밍]]
