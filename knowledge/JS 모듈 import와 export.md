---
tags:
  - es-module
  - import
  - export
---
`import` 문에 중괄호가 붙는지 안 붙는지는 **취향이 아니라 export 방식이 결정**한다.

| export 방식 | 개수 | import 문법 | 이름 변경 |
| --- | --- | --- | --- |
| `export default` | 파일당 **하나** | `import Board from './Board'` | **자유** |
| `export` (named) | 여러 개 | `import { Board, List } from './Board'` | `as`로만 가능 |

- `export default`는 파일이 내보내는 것이 하나뿐이라 **받는 쪽에서 이름을 마음대로 지어도 된다.**
- named export는 이름으로 골라 꺼내는 방식이라 **중괄호 안에 가져올 대상을 정확히 적어야 한다.**

## 전부 가져오기 — `import * as`
named export가 여러 개일 때 하나씩 나열하는 대신 통째로 가져와 네임스페이스처럼 쓴다.

```javascript
import * as S from './styles';

<S.Wrapper>
  <S.Header></S.Header>
</S.Wrapper>
```

스타일 컴포넌트처럼 **같은 성격의 것을 여러 개 내보내는 파일**에서 특히 유용하다. `S.`이라는 접두사가 붙어 **어디서 온 컴포넌트인지 한눈에 구분**된다.

## 관련 노트
- [[container-presentational 패턴]] — `import * as S`가 실제로 쓰이는 곳
- [[React]]
