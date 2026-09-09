---
tags:
  - react
  - props
---
컴포넌트를 역할별로 쪼개면 값과 함수를 건네줄 통로가 필요해진다. ==props는 부모 컴포넌트가 자식 컴포넌트에게 값을 전달하는 수단==이며, **객체로 만들어져 `key: value` 형식**으로 넘어간다.

```javascript
// 부모 (container.js)
return (
  <BoardListUI
    boards={boards}
    best={best}
  />
);
```

```javascript
// 자식 (presenter.js)
export default function BoardListUI(props) {
  return (
    <>
      {props.boards}
      {props.best}
    </>
  );
}
```

## 구조 분해 할당으로 받기
`props.`를 매번 붙이지 않으려면 인자 자리에서 바로 분해한다.

```javascript
export default function BoardListUI({ boards, best }) {
  return (
    <>
      {boards}
      {best}
    </>
  );
}
```

어떤 props를 쓰는지 **함수 시그니처만 봐도 드러난다**는 게 실질적인 이점이다.

## 값뿐 아니라 함수도 넘어간다
props로 함수를 내려보내면 자식이 부모의 상태를 바꿀 수 있다. 이것이 [[React State 끌어올리기]]의 원리다.

## 관련 노트
- [[React State 끌어올리기]] — props로 setter를 내려보내는 패턴
- [[container-presentational 패턴]] — props가 필요해지는 구조적 이유
- [[props.children과 레이아웃 컴포넌트]] — 이름을 주지 않아도 넘어가는 특수한 props
- [[CSS-in-JS와 Emotion]] — props로 스타일을 분기시키기
- [[React]]
