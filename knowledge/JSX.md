---
tags:
  - react
  - jsx
---
JSX는 **React 전용 HTML**, 정확히는 ==JavaScript의 확장 문법==이다. HTML처럼 생겼지만 JavaScript로 컴파일되므로, HTML의 예약어와 충돌하는 속성 이름이 바뀐다.

## HTML과 달라지는 지점
```html
<!-- 기존 HTML -->
<div>
  <div class="title">제목</div>
  <button onclick="alert()">버튼</button>
</div>

<!-- JSX -->
<div>
  <div className="title">제목</div>
  <button onClick={alert}>버튼</button>
</div>
```

- `class` → **`className`** (`class`가 JavaScript 예약어라서)
- 이벤트 속성은 **camelCase** (`onclick` → `onClick`)
- 중괄호 `{}` 안은 JavaScript 표현식 영역

## style 속성은 중괄호 두 개
```html
<div style={{ color: 'red' }}>hello</div>
```

바깥 `{}`는 **JSX 안의 JavaScript 영역**, 안쪽 `{}`는 **객체 리터럴**이다. 두 개가 겹쳐 보이는 것이지 문법이 특별한 게 아니다.

## 관련 노트
- [[React 컴포넌트 - 클래스형과 함수형]] — JSX를 반환하는 주체
- [[React Fragment]] — 최상위 노드를 하나로 묶는 방법
- [[CSS-in-JS와 Emotion]] — JSX에 스타일을 붙이는 다른 방식
- [[React]]
