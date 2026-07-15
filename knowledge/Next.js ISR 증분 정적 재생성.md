---
tags:
  - nextjs
  - isr
---

**ISR(Incremental Static Regeneration, 증분 정적 재생성)** 은 "정적 페이지(SSG)의 압도적인 속도"와 "서버 렌더링(SSR)의 데이터 유연성"을 결합한 기법이다. 페이지 **전체를 빌드하지 않고**, 필요한 시점에 정적 페이지를 **점진적으로 생성·갱신**한다.

## 동작 원리 (Pages Router 기준)

동적 라우팅(`pages/posts/[id].js`)에서 ISR은 세 가지 장치로 동작한다.

1. **일부만 선(先) 빌드 — `getStaticPaths`**
   빌드 시점에 모든 상세 페이지를 만들면 빌드 시간이 너무 길어진다. 그래서 인기 글·최신 글 등 **일부 ID만 지정**해 정적 HTML로 미리 구워둔다.

2. **새 페이지 실시간 생성 — `fallback: 'blocking'`**
   미리 빌드하지 않은 페이지에 사용자가 **처음 접속**하면, 그 순간 서버가 실시간으로 HTML을 생성(SSR처럼 동작)해 보여준다. 동시에 이 결과를 정적 파일로 **캐싱**해, 다음 접속자에게는 정적 페이지로 응답한다.

3. **백그라운드 주기적 최신화 — `revalidate`**
   설정 시간(예: 60초)이 지난 뒤 접속하면, Next.js는 대기 없이 **캐싱된 이전 HTML을 즉시** 보여주고, **백그라운드에서 조용히 데이터를 다시 불러와 HTML을 갱신**해 둔다. 그 다음 접속자부터 업데이트된 화면을 본다.

> [!info]
> `revalidate`의 핵심은 ==stale-while-revalidate== 전략이다 — 사용자를 기다리게 하지 않고 **일단 오래된 캐시를 보여준 뒤 뒤에서 갱신**하므로 속도와 최신성을 동시에 챙긴다.

## App Router에서는

Next.js 13의 App Router부터 `getStaticPaths`·`revalidate` 옵션이 폐지되고, `fetch`의 캐싱 옵션으로 통합되었다. ISR은 이제 `fetch(url, { next: { revalidate: 60 } })` 한 줄로 구현한다. → [[Next.js Pages Router에서 App Router로 렌더링 패러다임 전환]]

## 관련 노트

- [[Next.js Pages Router에서 App Router로 렌더링 패러다임 전환]] — ISR을 포함한 렌더링 방식이 라우터별로 어떻게 구현되는지 매핑
