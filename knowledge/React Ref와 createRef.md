---
tags:
  - react
  - ref
---
==Ref는 HTML 태그(DOM 노드)를 변수에 담아 직접 다루는 수단==이다. React는 보통 state로 화면을 제어하지만, 포커스·스크롤·미디어 재생처럼 **DOM API를 직접 호출해야 하는 일**은 state로 표현할 수 없다.

```javascript
// 1. ref 객체 생성 (초기값 null)
inputRef = createRef<HTMLInputElement>(null);

// 2. 태그에 연결
<input type="text" ref={this.inputRef} />

// 3. 마운트 이후에 접근
componentDidMount() {
  this.inputRef.current?.focus();
}
```

> [!warning]
> `ref.current`는 **화면이 그려진 뒤에야 채워진다.** `render` 도중이나 생성 시점에 접근하면 `null`이므로, `componentDidMount`(함수형은 `useEffect`) 이후에 써야 하고 옵셔널 체이닝(`?.`)으로 방어한다.

함수형 컴포넌트에서는 `createRef` 대신 `useRef`를 쓴다. `createRef`는 렌더링마다 새 객체를 만들지만 `useRef`는 값을 유지한다.

## 관련 노트
- [[React 컴포넌트 생명주기]] — `current`가 채워지는 시점
- [[React]]
