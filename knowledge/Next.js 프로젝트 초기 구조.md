---
tags:
  - nextjs
  - boilerplate
  - package-json
---
`npx create-next-app@latest`로 프로젝트를 만들면 **보일러플레이트(초기 폴더 구조)**가 생성된다.

```text
CODECAMP_FRONTEND/
├── node_modules/     # 라이브러리 / 프레임워크 저장소
├── pages/            # frontend 페이지 화면들
├── public/           # 사진, 아이콘
├── styles/           # css 파일
├── .gitignore        # git에서 제외할 파일
├── package.json      # 기본 매뉴얼
├── README.md         # 상세 설명서
└── yarn.lock         # 버전 잠금 파일
```

> [!info]
> `pages/` 폴더가 곧 URL 경로가 된다 — [[Next.js 동적 라우팅]]. `public/`에 넣은 파일은 `/파일명`으로 바로 접근된다.

## package.json — 프로젝트의 기본 매뉴얼
세 덩어리로 읽으면 된다.

```json
{
  "name": "codecamp_frontend_user",     // ── 기본 정보
  "version": "0.1.0",
  "private": true,

  "scripts": {                          // ── 실행 명령어
    "dev": "next dev",
    "build": "next build",
    "start": "next start"
  },

  "dependencies": {                     // ── 라이브러리 / 프레임워크
    "@apollo/client": "^3.3.11",
    "@emotion/react": "^11.1.5",
    "@emotion/styled": "^11.1.5",
    "@material-ui/core": "^4.11.3",
    "antd": "^4.13.1",
    "graphql": "^15.5.0",
    "next": "10.0.8",
    "react": "17.0.1",
    "react-dom": "17.0.1"
  }
}
```

| 키 | 의미 |
| --- | --- |
| `name` / `version` / `private` | 기본 정보 |
| `scripts` | `yarn dev` 처럼 실행할 명령어 정의 |
| `dependencies` | 설치된 라이브러리와 **버전 범위** |

## 자주 쓰는 라이브러리 설치
```shell
# Emotion (CSS-in-JS)
yarn add @emotion/react @emotion/styled

# Apollo Client + GraphQL
npm install @apollo/client graphql

# UI 라이브러리
yarn add antd
npm install @material-ui/core

# HTTP 클라이언트
yarn add axios
```

## 관련 노트
- [[Node.js와 npm 패키지 매니저]] — `node_modules`와 락 파일이 생기는 배경
- [[container-presentational 패턴]] — 기본 구조 위에 얹는 폴더 설계
- [[Next.js와 SEO]]
