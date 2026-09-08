---
tags:
  - java
  - array
  - vector
  - collection
---
`Array`와 `Vector`는 여러 값을 묶는다는 점은 같지만 **제약이 정반대**다.

| | 담을 수 있는 타입 | 크기 |
| --- | --- | --- |
| **Array** | **같은 데이터 타입**만 | 고정 |
| **Vector** | **다른 타입도** 가능 | **변경 가능** |

## Array
```java
String[] args;      // args의 data type은 String array이고
                    // args는 그 배열을 관리하는 식별자다

intArray.length     // 길이
intArray[0]         // 인덱스 접근
```

다차원 배열은 배열의 배열이므로 `intArray[1][2].length`처럼 각 차원마다 길이를 가진다.

![[java-multidimensional-array.png]]

## Vector
소프트웨어적 객체라서 크기가 유연하지만, **꺼낼 때 `Object`로 나오므로 캐스팅해야 한다.**

```java
Vector v = new Vector(10, 10);

v.add(Object obj);        // 어떤 타입이든 추가 가능
v.size();                 // 들어있는 값의 개수
v.elementAt(int i);       // 해당 인덱스 값 반환

Object obj = v.elementAt(i);
String s = (String) obj;  // 캐스팅 필요
```

## Generic `<>`
이 캐스팅 문제를 없애는 것이 제네릭이다. **담을 타입을 미리 못 박아** 꺼낼 때 캐스팅 없이 쓰게 한다.

![[java-generic.png]]

## 관련 노트
- [[Java Reference 형 변환]]
- [[Java Wrapper Class와 오토박싱]]
- [[Java 반복문]]
- [[Java]]
