---
tags:
  - java
  - inheritance
  - generalization
  - object-modeling
  - is-a-relationship
---
상속을 네 개의 동사로 나눠 보면 관계가 분명해진다. `class 코끼리, 독수리, 고래 extends 동물`을 예로 들면:

| 개념 | 설명 |
| --- | --- |
| **일반화** | 코끼리·독수리·고래의 공통 속성을 뽑아 "동물"이라 이름 붙인 것 |
| **구체화** | 각 동물만 가진 상태·속성을 확장(추가)한 것 |
| **상속** | 구체적 클래스가 가진 것을 일반적 클래스도 가지고 있음 |
| **계층화** | 하위는 상위를 대신할 수 있지만 **상위는 하위를 대신할 수 없음** → ==`~ is a ~` 관계== |

> [!tip]
> **일반적 클래스를 먼저 만들고 그것을 공유해 구체적 클래스를 만드는 것**이 효율적인 Object Modeling이다.

![[java-generalization.png]]

## 다른 관계들
상속(`is a`)만 관계인 것은 아니다. **Association**은 `~ has a ~` 관계로, 한 객체가 다른 객체를 **가지고 있는** 구조다.

![[java-oop-relationships.png]]

## 관련 노트
- [[Java Reference 형 변환]]
- [[Java super와 this]]
- [[Java Interface와 다중상속 보완]]
- [[시스템 개발 절차 - 모델링과 프로그래밍]]
