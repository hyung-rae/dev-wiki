---
tags:
  - java
  - scanner
  - buffer
  - stdin
  - import
---
`Scanner`는 Java 라이브러리가 제공하는 **각종 입력을 담당하는 클래스**다. 키보드 입력뿐 아니라 **파일 입력, 흐름 입력**도 처리한다. 기본 제공 패키지가 아니라서 **`import java.util.Scanner;`로 가져와야** 한다.

## 동작 방식: 버퍼를 거친다
입력된 데이터를 프로그램 변수에 **곧장 넣지 않는다.** ==버퍼 메모리라는 임시 저장소==에 담아 올바른 데이터인지 확인한 뒤에야 변수에 저장한다. 그래서 다 쓰고 나면 **`close()`로 자원을 정리**하는 것이 좋다.

```java
Scanner scanner = new Scanner(System.in);

int number = scanner.nextInt();
double number2 = scanner.nextDouble();

scanner.nextLine();               // 버퍼 초기화
String name = scanner.nextLine();

scanner.close();
```

> [!warning]
> **`nextInt()` 다음에 바로 `nextLine()`을 부르면 빈 문자열이 돌아온다.** 앞선 입력의 개행 문자가 버퍼에 남아 있어 "사용자가 아무것도 입력하지 않고 끝냈다"고 착각하기 때문이다. `nextLine()`을 한 번 헛돌려 **버퍼를 비우고** 진짜 입력을 받는다.

## 관련 노트
- [[Java 콘솔 출력 - print println printf]]
- [[Java IO 패키지와 Stream]]
- [[Java]]
