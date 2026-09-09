---
tags:
  - react
  - class-component
  - this-binding
---
`Component`를 상속받아 만드는 컴포넌트. 함수형과 달리 **state를 객체 하나로 묶어 관리**하고, `render()`가 JSX를 반환한다.

```javascript
import { Component } from "react";

export default class MyCounterPage extends Component {
  // state는 객체로 묶어 선언한다. setState는 Component가 제공하므로 선언 불필요
  state = {
    count: 0,
  };

  onClickCounter = () => {
    this.setState((prev) => ({
      count: prev.count + 1,
    }));
  };

  render() {
    return (
      <>
        <div>현재카운트 : {this.state.count}</div>
        <button onClick={this.onClickCounter}>+</button>
      </>
    );
  }
}
```

## 규칙
- state는 **객체로 선언**하므로 `setState({ ... })`도 **객체로 넘겨야** 한다
- 클래스 안에서 메서드를 선언할 땐 `function` 키워드를 뺀다
- 화면은 반드시 `render()`의 `return`으로 그린다

## this 바인딩 문제
```javascript
// 일반 메서드로 선언하면 함수 안의 this가 window를 가리켜 에러가 난다
onClickCounter() {
  console.log(this.state.count);
}
// → 호출부에서 bind가 필요하다
<button onClick={this.onClickCounter.bind(this)}>+</button>

// 화살표 함수로 선언하면 상위 스코프의 this를 그대로 쓰므로 bind가 필요 없다
onClickCounter = () => {
  console.log(this.state.count);
};
<button onClick={this.onClickCounter}>+</button>
```

> [!warning]
> ==클래스 메서드의 `this`는 호출 방식에 따라 결정된다.== 이벤트 핸들러로 넘기면 인스턴스와의 연결이 끊어지므로, **화살표 함수로 선언**하는 편이 안전하다.

## 관련 노트
- [[React 컴포넌트 - 클래스형과 함수형]] — 두 형태의 위치
- [[React 컴포넌트 생명주기]] — 클래스형에서만 쓰는 생명주기 메서드
- [[setState의 prev - 함수형 업데이트]] — `this.setState`에도 동일하게 적용
- [[React]]
