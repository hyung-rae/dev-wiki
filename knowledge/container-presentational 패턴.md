---
tags:
  - react
  - container-presentational
  - frontend-architecture
---
==기능 역할(JavaScript)과 UI 역할(JSX)을 파일로 분리하는 React의 대표적 패턴==이다. 한 페이지를 역할별 파일로 쪼갠다.

| 파일 | 역할 | 하는 일 |
| --- | --- | --- |
| `index.js` | page | URL 경로에 대응하는 페이지. `container.js`를 import해서 보여준다 |
| `container.js` | javascript | 로직 담당. `presenter.js`를 import해 UI를 구성한다 |
| `presenter.js` | view (JSX) | UI만 그린다. `styles.js`에서 CSS-in-JS를 가져온다 |
| `queries.js` | graphql | `container.js`가 쓰는 GraphQL 쿼리 모음 |
| `styles.js` | css (emotion) | CSS-in-JS 스타일 컴포넌트 정의 |

`container` → `presenter` 방향으로만 흐르고, 둘 사이는 [[React props와 구조 분해 할당]]으로 연결된다.

```javascript
// container.js — 로직에서 만든 값을 내려보낸다
return <BoardListUI boards={boards} best={best} />;
```

```javascript
// presenter.js — 받아서 그리기만 한다
export default function BoardListUI({ boards, best }) {
  return <S.Wrapper>{boards}</S.Wrapper>;
}
```

> [!info]
> UI 컴포넌트를 원자 단위부터 조합하는 **Atomic Design**과 결이 다르다. container/presentational은 **한 화면 안에서 로직과 뷰를 가르는** 축이고, Atomic Design은 **컴포넌트의 크기 계층**을 나누는 축이다.

Hook이 등장하면서 로직을 커스텀 훅으로 빼는 방식이 일반화되어, 파일을 물리적으로 가르는 이 패턴의 필요성은 예전보다 줄었다.

## 관련 노트
- [[React props와 구조 분해 할당]] — container와 presenter를 잇는 통로
- [[프론트엔드 폴더 구조 - FSD vs Co-location]] — 프로젝트 전체 규모의 폴더 설계
- [[JS 모듈 import와 export]] — `styles.js`를 통째로 가져오는 방식
- [[React]]
