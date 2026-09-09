---
tags:
  - react
  - state
  - props
  - lifting-state-up
---
React의 데이터 흐름은 부모 → 자식으로만 흐르는 ==하향식 단방향 데이터 흐름==이다. 그래서 **형제 컴포넌트끼리는 직접 값을 주고받을 수 없다.**

해결책은 **공유해야 할 state를 공통 부모로 끌어올리고**, 부모가 `state`와 함께 ==그 state를 바꿀 수 있는 함수까지 props로 내려주는== 것이다. 그러면 자식이 부모의 state를 바꿀 수 있다.

```javascript
// 부모 컴포넌트
export default function StateUpPage() {
  const [count, setCount] = useState(0);

  const onClickCounter = () => {
    setCount((prev) => prev + 1);
  };

  return (
    <>
      <Child1 count={count} onClickCounter={onClickCounter} />
      <Child2 count={count} onClickCounter={onClickCounter} />
    </>
  );
}
```

```javascript
// 자식 컴포넌트
export default function Child1(props) {
  return (
    <>
      <div>Child1 Count : {props.count}</div>
      <button onClick={props.onClickCounter}>+</button>
    </>
  );
}
```

두 자식이 **같은 state를 바라보므로** 한쪽에서 올린 카운트가 다른 쪽에도 즉시 반영된다.

> [!tip]
> `setState`를 그대로 내려주지 않고, **부모가 정의한 변경 함수**를 내려줘도 된다. 오히려 이쪽이 변경 로직을 부모에 가둬둘 수 있어 안전하다.

## 관련 노트
- [[React state와 useState]] — 끌어올릴 대상인 state
- [[React props와 구조 분해 할당]] — 값과 함수를 내려보내는 통로
- [[setState의 prev - 함수형 업데이트]]
- [[React]]
