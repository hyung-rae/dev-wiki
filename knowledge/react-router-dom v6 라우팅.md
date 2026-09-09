---
tags:
  - react
  - react-router-dom
  - routing
---
React 자체에는 라우팅 기능이 없다. SPA에서 경로별로 다른 화면을 보여주려면 `react-router-dom` 같은 라이브러리로 **직접 라우터를 구성**해야 한다.

## v6에서 바뀐 점
`Switch`가 `Routes`로 바뀌었고, 렌더링할 컴포넌트를 ==`component`/`render` prop이 아니라 `element`에 JSX로== 넘긴다.

```javascript
import { BrowserRouter, Route, Routes } from "react-router-dom";
import { Main, Page1, Page2, NotFound } from "../pages";
import { Header } from ".";

const Router = () => {
  return (
    <BrowserRouter>
      <Header />
      <Routes>
        <Route path="/" element={<Main />} />
        <Route path="/page1/*" element={<Page1 />} />
        <Route path="/page2/*" element={<Page2 />} />
        <Route path="/*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
};

export default Router;
```

- `<BrowserRouter>` — 라우팅 컨텍스트를 제공하는 최상위 래퍼
- `<Routes>` 밖에 둔 `<Header />`는 **경로가 바뀌어도 유지**된다
- `path="/*"`를 맨 아래 두어 **404 처리**

> [!info]
> Next.js는 `pages`(또는 `app`) 폴더 구조가 곧 경로가 되는 **파일 기반 라우팅**이라 이 라이브러리가 필요 없다.

## 관련 노트
- [[Next.js Router 객체]] — 파일 기반 라우팅에서의 페이지 이동
- [[React]]
