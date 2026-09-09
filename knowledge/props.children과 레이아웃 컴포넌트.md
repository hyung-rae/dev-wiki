---
tags:
  - react
  - props-children
  - layout
---
레이아웃 설계의 출발점은 ==변하지 않는 부분과 변하는 부분을 나누는 것==이다. 헤더·배너·네비게이션·푸터는 고정이고, 가운데 본문만 페이지마다 바뀐다.

이때 **여는 태그와 닫는 태그 사이에 넣은 내용은 자동으로 `props.children`으로 전달된다.** 이름을 직접 지어주지 않아도 된다.

```javascript
// _app.tsx — 모든 페이지를 Layout으로 감싼다
function MyApp({ Component, pageProps }) {
  return (
    <ApolloProvider client={client}>
      <Global styles={globalStyles} />
      <Layout>
        <Component {...pageProps} />
      </Layout>
    </ApolloProvider>
  );
}
```

```javascript
// Layout — 감싼 내용이 props.children으로 들어온다
interface ILayoutProps {
  children: ReactChild;
}

export default function Layout(props: ILayoutProps) {
  return (
    <Wrapper>
      <Header />
      <Banner />
      <Navigation />
      <Body>{props.children}</Body>
      <Footer />
    </Wrapper>
  );
}
```

## 레이아웃 폴더 구조
공통 UI는 한 폴더에 모아두고 `index.tsx`로 묶어 내보낸다.

```text
src/
└── components/
    └── commons/
        ├── buttons/
        └── layout/
            ├── banner/
            ├── footer/
            ├── header/
            ├── navigation/
            ├── sidebar/
            └── index.tsx
```

## 일부 페이지만 레이아웃 빼기
로그인 페이지처럼 헤더가 없어야 하는 화면은 **현재 경로로 조건부 렌더링**한다.

```javascript
const HIDDEN_HEADERS = ["/12-05-modal-address-state-prev", "/12-04-state-prev"];
const isHiddenHeader = HIDDEN_HEADERS.includes(router.asPath);

{!isHiddenHeader && <Header>여기는 헤더 영역</Header>}
```

## 관련 노트
- [[React props와 구조 분해 할당]] — `children`도 결국 props다
- [[Next.js Router 객체]] — 조건부 렌더링에 쓰는 `router.asPath`
- [[Emotion 전역 스타일 적용]] — 같은 `_app.tsx`에서 함께 설정한다
- [[React]]
