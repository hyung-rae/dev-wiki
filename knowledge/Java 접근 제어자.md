---
tags:
  - java
  - access-modifier
  - encapsulation
  - singleton
---
접근 제어자는 ==Encapsulation(캡슐화)을 언어 차원에서 지원==하는 장치다. 어디까지 이 멤버를 보여줄지 정한다.

![[java-access-modifier.png]]

## private 생성자
생성자를 `private`으로 막으면 **아무도 인스턴스를 생성할 수 없다.** 두 가지 활용법이 있다.

1. **상태값과 메서드를 전부 `static`으로** 만들어 생성자 없이 사용
2. **자기 클래스 안에 인스턴스를 리턴하는 메서드**를 만들어 그 통로로만 제공

```java
public class Test {

    private Test() {
    }

    public static Test getInstance() {
        return new Test();
    }
}
```

> [!info]
> 2번이 **싱글턴 패턴**의 뼈대다. 생성 경로를 하나로 좁혀 클래스가 인스턴스 생성을 직접 통제한다.

## 관련 노트
- [[Java static final abstract 제어자]]
- [[Java 클래스 구성과 Inner Class]]
- [[Java 객체지향의 관계 - 계층화와 일반화]]
