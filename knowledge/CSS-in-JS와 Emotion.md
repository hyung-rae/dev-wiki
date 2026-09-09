---
tags:
  - react
  - css-in-js
  - emotion
---
==CSS-in-JS는 스타일을 별도 `.css` 파일이 아니라 JavaScript 안에서 컴포넌트로 정의하는 방식==이다. React 진영에서는 **Emotion**을 많이 쓴다.

| | 기존 CSS | CSS-in-JS |
| --- | --- | --- |
| 정의 위치 | `.css` 파일 | `.ts`/`.js` 파일 |
| 사용 | `<div className={styles.title}>` | `<Title>` |
| 스코프 | 클래스명 충돌 가능 | 컴포넌트에 묶여 격리 |
| 동적 값 | 클래스 토글로 처리 | **props로 직접 분기** |

```css
/* 기존 CSS */
.title {
  width: 996px;
  height: 52px;
}
```

```javascript
/* CSS-in-JS */
import styled from '@emotion/styled';

export const Title = styled.div`
  width: 996px;
  height: 52px;
`;
```

```html
<Title>hello</Title>
```

## props로 스타일 분기하기
CSS-in-JS의 가장 큰 이점. 스타일 값 자리에 함수를 넣으면 **props를 받아 값을 계산**한다.

```javascript
<MyButton onClick={props.editBoard} change={props.myChange}>
  게시물 수정하기!
</MyButton>
```

```javascript
export const MyButton = styled.button`
  background-color: ${(props) => (props.change === true ? "gray" : "yellow")};
  font-size: 30px;
`;
```

스타일 컴포넌트는 보통 `styles.js`에 모아두고 [[JS 모듈 import와 export]]의 `import * as S` 형태로 가져다 쓴다.

## 관련 노트
- [[JSX]] — 스타일을 붙일 대상
- [[React props와 구조 분해 할당]] — 스타일 분기에 쓰이는 props
- [[Emotion 전역 스타일 적용]] — 프로젝트 전체에 걸리는 스타일
- [[React]]
