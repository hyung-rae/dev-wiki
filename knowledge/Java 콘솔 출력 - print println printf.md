---
tags:
  - java
  - console-output
  - printf
  - format-specifier
---
`System.out`의 출력 메서드 셋은 **다음 출력이 어디서 시작되는가**로 갈린다.

| 메서드 | 뜻 | 출력 후 커서 위치 |
| --- | --- | --- |
| `print()` | — | 같은 줄 오른쪽 다음 칸 |
| `println()` | print **a line** | 다음 줄 첫 칸 |
| `printf()` | print **in format** | 같은 줄 오른쪽 다음 칸 |

## 이스케이프 문자
`\`와 합쳐져 한 문자가 되는 특수 문자들.

| 표기 | 의미 |
| --- | --- |
| `\n` | 줄바꿈 |
| `\t` | 탭 공백 |
| `\"` | 문자로서의 큰따옴표 |

## printf 서식 문자
`%` 뒤에 **[정렬][자릿수][.소수점자리] + 타입문자** 순으로 붙인다.

```java
int number = 10;
System.out.printf("%5d\n",  number);   // "   10"  5자리 오른쪽 정렬
System.out.printf("%-5d\n", number);   // "10   "  왼쪽 정렬 (- 붙임)
System.out.printf("%05d\n", number);   // "00010"  빈자리 0 채움

number = 270;
System.out.printf("%x\n", number);     // 10e   16진수 소문자
System.out.printf("%X\n", number);     // 10E   16진수 대문자

double d = 2.4739;
System.out.printf("%.2f\n", d);        // 2.47        소수점 2자리
System.out.printf("%15.2f\n", d);      // "           2.47"

System.out.printf("%S\n", "abc");      // ABC   대문자로
```

> [!warning]
> `printf`의 실패 조건 — **잘못된 `%` 문자**, **넘긴 값과 `%` 타입 불일치**, **`%` 개수보다 값이 적을 때**는 에러가 난다. 반대로 값이 더 많은 것은 문제되지 않는다.

## 관련 노트
- [[Java Scanner와 버퍼 메모리]]
- [[Java 산술 연산자]]
- [[Java]]
