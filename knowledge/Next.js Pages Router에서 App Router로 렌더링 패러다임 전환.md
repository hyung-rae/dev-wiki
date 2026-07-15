---
tags:
  - nextjs
  - app-router
---

Next.js 13의 **App Router**에서는 `getStaticProps`·`getServerSideProps`·`getStaticPaths` 같은 **페이지 수준 API가 완전히 폐지**되었다. 대신 리액트 서버 컴포넌트(RSC) 위에서 **표준 `fetch` API의 옵션을 제어하는 방식**으로 단순화되었다.

핵심은 고민의 층위가 바뀐 것이다.

- **Pages Router**: "이 페이지엔 어떤 **함수**(`getServerSideProps` vs `getStaticProps`)를 쓸까?" → **페이지 수준**의 고민
- **App Router**: 모든 페이지가 기본적으로 서버 컴포넌트이며, "가져올 **데이터(`fetch`)** 를 얼마나 자주 갱신할까?" → **데이터 수준**의 고민

## 렌더링 개념 매핑

| 기능 | Pages Router (기존) | App Router (현재) | 구현 방식 (App Router) |
| --- | --- | --- | --- |
| **SSG** | `getStaticProps` | 정적 렌더링 | `fetch('url')` (기본 캐싱) |
| **SSR** | `getServerSideProps` | 동적 렌더링 | `fetch('url', { cache: 'no-store' })` |
| **ISR** | `revalidate: 60` 옵션 | 시간 기반 재검증 | `fetch('url', { next: { revalidate: 60 } })` |
| **동적 경로 정의** | `getStaticPaths` | 정적 파라미터 생성 | `generateStaticParams()` 함수 export |

## 구현 예시 — `app/posts/[id]/page.js`

페이지 컴포넌트 자체가 서버에서 실행되는 **서버 컴포넌트**이므로, 컴포넌트 내부에서 `async/await` + `fetch`로 직접 데이터를 가져온다.

```javascript
// 1. 빌드 시점에 미리 생성할 동적 경로 지정 (getStaticPaths의 역할)
export async function generateStaticParams() {
  return [{ id: '1' }, { id: '2' }, { id: '3' }];
}

// 2. 서버 컴포넌트 본문
export default async function PostDetailPage({ params }) {
  const { id } = params;

  // fetch 옵션에 revalidate만 주면 ISR이 적용된다.
  const res = await fetch(`https://api.example.com/posts/${id}`, {
    next: { revalidate: 60 }, // 60초마다 백그라운드 갱신
  });
  const post = await res.json();

  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </article>
  );
}
```

> [!tip]
> SSG·SSR·ISR을 별도 함수로 나누지 않고 **`fetch` 옵션 하나로 전환**하므로 코드가 훨씬 깔끔하고 직관적이다.

## 관련 노트

- [[Next.js ISR 증분 정적 재생성]] — 위 매핑에서 ISR이 실제로 어떻게 동작하는지(부분 빌드·재검증)
