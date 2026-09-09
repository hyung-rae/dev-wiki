---
tags:
  - react
  - emotion
  - global-style
---
컴포넌트 단위 스타일과 별개로, `margin` 초기화나 폰트처럼 **프로젝트 전체에 한 번만 걸어야 하는 스타일**이 있다. Emotion은 `Global` 컴포넌트로 이를 처리한다.

```text
src/
└── commons/
    └── styles/
        └── globalStyles.ts
```

```javascript
// globalStyles.ts
import { css } from "@emotion/react";

import "slick-carousel/slick/slick.css";        // 프로젝트 전체에서 쓰는 css 임포트
import "slick-carousel/slick/slick-theme.css";

export const globalStyles = css`
  * {
    margin: 0px;
    box-sizing: border-box;
  }

  @font-face {
    font-family: "mainFont";
    src: url("/fonts/DoHyeon-Regular.ttf");   /* public 폴더 기준 경로 */
  }
`;
```

```javascript
// _app.tsx — 최상단에 한 번만 선언한다
import { Global } from "@emotion/react";

return (
  <ApolloProvider client={client}>
    <Global styles={globalStyles} />
    <Layout>
      <Component {...pageProps} />
    </Layout>
  </ApolloProvider>
);
```

> [!tip]
> 직접 올린 폰트는 **경량화된 파일**을 쓴다. Google Fonts는 이미 웹에 최적화되어 있어 그대로 써도 된다.

## 관련 노트
- [[CSS-in-JS와 Emotion]] — 컴포넌트 단위 스타일
- [[props.children과 레이아웃 컴포넌트]] — 같은 `_app.tsx`에서 함께 설정
- [[React]]
