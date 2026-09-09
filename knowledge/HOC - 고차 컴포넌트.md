---
tags:
  - react
  - hoc
---
==HOC(high order components, 고차 컴포넌트)는 컴포넌트를 인자로 받아 새 컴포넌트를 반환하는 함수==다. 감싼 쪽이 **먼저 실행되므로**, 원본이 그려지기 전에 공통 처리를 끼워 넣을 수 있다.

```javascript
// 컴포넌트를 받아서, 컴포넌트를 돌려준다
const withSomething = (Component) => (props) => {
  // 원본이 그려지기 전에 할 공통 처리

  return <Component {...props} />;
};
```

```javascript
// 사용하는 쪽 — export할 때 감싼다
export default withAuth(MyPage);
```

인증 검사처럼 **여러 페이지에 똑같이 들어가는 로직**을 페이지마다 복붙하지 않고 한곳에 모을 때 쓴다.

> [!tip]
> HOC는 이름 앞에 **`with`를 붙이는 것이 관례**다 (`withAuth.tsx`, `withRouter`).

동작 원리는 함수가 함수를 반환하는 [[고차 함수와 클로저]] 구조 그대로다. 반환된 컴포넌트가 원본 `Component`와 `props`를 클로저로 붙잡고 있기 때문에 감싸기가 성립한다.

## 관련 노트
- [[고차 함수와 클로저]] — HOC가 서 있는 문법 기반
- [[React 컴포넌트 - 클래스형과 함수형]]
- [[React]]
