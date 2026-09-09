---
tags:
  - react
  - component
  - functional-component
---
React는 UI와 기능을 **컴포넌트 단위로 모듈화**해서 재사용성과 효율을 높이는 라이브러리다. 같은 코어를 어디에 얹느냐에 따라 결과물이 달라진다.

| 조합 | 결과물 |
| --- | --- |
| React.js | 웹 |
| React Native | 앱 (크로스 플랫폼) |
| React + Electron | PC 앱 |

## 클래스형 → 함수형
React는 처음에 **==클래스형 컴포넌트==만** 있었고, 이후 더 간결한 **==함수형 컴포넌트==**가 등장해 표준이 되었다.

```javascript
// 클래스형
import { Component } from 'react';

class New extends Component {
  render() {
    // JavaScript 작성 공간
    return (
      // JSX 작성 공간
    );
  }
}

export default New;
```

```javascript
// 함수형
function New() {
  // JavaScript 작성 공간
  return (
    // JSX 작성 공간
  );
}

export default New;

// 화살표 함수도 가능
const New = () => {
  return ();
};
```

두 형태의 결정적 차이는 **문법이 아니라 상태·생명주기를 다루는 방식**이다. 클래스형은 `this.state`와 생명주기 메서드를, 함수형은 Hook을 쓴다.

> [!info]
> 현재 새로 작성하는 코드는 함수형이 기본이다. 클래스형은 레거시 코드를 읽을 때 필요하다.

## 관련 노트
- [[JSX]] — 컴포넌트가 `return`하는 것
- [[React 클래스 컴포넌트]] — 클래스형의 state·`this` 처리
- [[React state와 useState]] — 함수형의 상태 관리
- [[React]]
