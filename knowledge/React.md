---
tags:
  - react
  - moc
---
React 학습 노트의 목차. 아래로 갈수록 앞의 개념을 전제로 한다.

## 기초
- [[React 컴포넌트 - 클래스형과 함수형]] — 모듈화의 단위, 두 작성 형태
- [[JSX]] — `class`가 `className`이 되는 이유
- [[React Fragment]] — `<>`에 `key`를 줄 수 없는 이유

## 상태
- [[React state와 useState]] — 직접 대입하면 화면이 안 바뀐다
- [[setState의 prev - 함수형 업데이트]] — setter를 연속 호출했을 때의 함정
- [[React State 끌어올리기]] — 하향식 단방향 흐름에서 형제끼리 값 공유하기

## 클래스 컴포넌트와 생명주기
- [[React 클래스 컴포넌트]] — state 객체와 `this` 바인딩
- [[React 컴포넌트 생명주기]] — 그린 후 / 변경될 때 / 사라질 때
- [[React Ref와 createRef]] — DOM을 변수에 담아 직접 다루기
- [[useEffect와 의존성 배열]] — 생명주기를 함수형에서 대체하기

## 컴포넌트 연결
- [[React props와 구조 분해 할당]] — 부모가 자식에게 값과 함수를 넘기는 통로
- [[props.children과 레이아웃 컴포넌트]] — 변하는 부분만 갈아끼우기
- [[HOC - 고차 컴포넌트]] — 렌더링 전에 공통 처리 끼워넣기

## 스타일
- [[CSS-in-JS와 Emotion]] — props로 스타일을 분기시키기
- [[Emotion 전역 스타일 적용]] — `Global`과 `@font-face`

## 구조와 라우팅
- [[container-presentational 패턴]] — 로직 파일과 뷰 파일 가르기
- [[react-router-dom v6 라우팅]] — SPA에서 라우터 직접 구성하기

## 함께 보기
- [[고차 함수와 클로저]] — HOC가 서 있는 JavaScript 문법
- [[JS 모듈 import와 export]] — 중괄호가 붙고 안 붙고의 기준
- [[프론트엔드 폴더 구조 - FSD vs Co-location]] — 프로젝트 규모에 따른 폴더 설계
- [[Next.js와 SEO]] — React 기반 프레임워크로 넘어가기
