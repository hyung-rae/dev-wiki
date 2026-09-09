---
tags:
  - react
  - fragment
---
컴포넌트는 **최상위 노드를 하나만** 반환할 수 있다. 의미 없는 `<div>`로 감싸면 DOM이 지저분해지므로, ==실제 DOM을 만들지 않고 묶기만 하는== `Fragment`를 쓴다.

```javascript
<Fragment>
  ...
</Fragment>

// 축약 문법
<>
  ...
</>
```

## 축약 문법에는 key를 줄 수 없다
```javascript
// map()에서 key가 필요하면 축약형(<>)을 쓸 수 없다
{items.map((item) => (
  <Fragment key={item.id}>
    <dt>{item.term}</dt>
    <dd>{item.desc}</dd>
  </Fragment>
))}
```

> [!warning]
> `<>`는 **props를 전혀 받지 못한다.** 리스트를 렌더링하면서 `key`를 줘야 한다면 반드시 `<Fragment>`를 명시적으로 써야 한다.

## 관련 노트
- [[JSX]] — Fragment가 필요해지는 이유(최상위 노드 제약)
- [[React]]
