---
tags:
  - nextjs
  - seo
  - moc
---
Next.js의 렌더링 전략과, 그 결과물이 검색엔진·크롤러에 어떻게 노출되는지에 대한 목차.

## 렌더링 전략
- [[Next.js Pages Router에서 App Router로 렌더링 패러다임 전환]] — 페이지 수준 API의 폐지
- [[Next.js ISR 증분 정적 재생성]] — SSG의 속도와 SSR의 유연성 결합

## 크롤러에 노출하기
- [[sitemap.xml]] — 크롤러에게 사이트 구조를 알리는 파일
- [[Next.js 사이트맵 자동 생성]] — `app/sitemap.ts` 내장 기능
- [[캐시 무효화 - URL 기반 캐싱]] — 크롤러가 옛 리소스를 계속 보는 이유
