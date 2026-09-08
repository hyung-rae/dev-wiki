---
tags:
  - java
  - io-package
  - stream
  - serializable
  - buffer
---
io package는 ==프로세스 외부로부터 data를 받고, 외부 프로세스에게 data를 주는 것==을 캡슐화한 클래스들이다.

## 특징
- **FIFO(Queue) 구조**
- **단방향 모델링** — 읽기 스트림과 쓰기 스트림이 따로다
- **io Block** — 데이터 입력을 기다리며 멈춘다
- 유연한 구조

![[java-io-stream-hierarchy.png]]

## 버퍼와 자원 정리
| 메서드 | 동작 |
| --- | --- |
| `close()` | 자원을 종료한다 / 버퍼 공간을 비운다 |
| `flush()` | 버퍼 공간의 data를 출력한다 |

## byte 계열 vs 문자 계열
```java
// 1byte씩 읽고 출력 — 한글이 깨진다
InputStream;
OutputStream;

// 문자 전용 Stream — 유니코드 지원
Reader r = new InputStreamReader();
Writer w = new OutputStreamWriter();
```

## SinkStream과 FilterStream
| | 역할 |
| --- | --- |
| **SinkStream** | data를 직접 주고받는 단순 입출력 |
| **FilterStream** | SinkStream으로 들어온 data를 **조작**한다. 더 구체적인 메서드를 쓰기 위해 감싼다 |

![[java-io-filter-stream.png]]

## Marker Interface
**인터페이스지만 오버라이딩이 필요 없다.** 구현할 메서드가 없고, "이 클래스는 이런 성격이다"라고 **표시(mark)** 하는 역할만 한다. `Serializable`이 대표적으로, 언젠가 직렬화해 외부로 보내거나 받아야 함을 뜻한다.

![[java-marker-interface.png]]

## 관련 노트
- [[Java Interface와 다중상속 보완]]
- [[Java Thread와 동기화]]
- [[Java Scanner와 버퍼 메모리]]
- [[Java]]
