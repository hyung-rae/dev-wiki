---
tags:
  - java
  - garbage-collection
  - reference-count
  - memory-management
---
Java는 메모리를 개발자가 직접 해제하지 않는다. **더 이상 참조되지 않는 객체를 런타임이 알아서 수거**한다.

판정 기준은 ==Reference Count가 0, 즉 "식별성이 없다"==는 것이다. 어떤 변수도 그 객체를 가리키고 있지 않으면 아무도 접근할 방법이 없고, garbage collector는 이런 것들을 **garbage로 인식해 수거·제거**한다.

![[java-garbage-collection.png]]

> [!info]
> 여기서 "식별성"은 [[Java Reference 형 변환|Reference]]가 붙어 있느냐를 말한다. 참조를 끊는 것(`obj = null`)이 곧 수거 대상으로 만드는 행위다.

## 관련 노트
- [[Java Reference 형 변환]]
- [[Java 플랫폼 독립성과 JVM]]
