---
tags:
  - nextjs
  - sitemap
  - static-export
---

Next.js에서 [[sitemap.xml]]을 만드는 방식은 **수동(`public` 폴더)**과 **내장 기능(`app/sitemap.ts`)** 두 가지가 있다. App Router(13+)부터는 내장 기능으로 빌드 시점에 자동 생성할 수 있다.

## 두 방식 비교

| 방식 | 동작 | 한계 |
| --- | --- | --- |
| `public/sitemap.xml` | `public` 폴더는 빌드 시 가공 없이 결과물(`out/`) 루트로 복사됨 | 페이지가 늘 때마다 **수동 수정**하거나 `next-sitemap` 같은 외부 패키지로 덮어써야 함 |
| `app/sitemap.ts` | 파일 규칙(convention)으로 **빌드 시점에 자동 생성** | 외부 패키지 불필요 |

> [!info]
> `public/sitemap.xml`에 두는 것 자체는 올바른 세팅이다. 다만 페이지 추가마다 손이 가는 게 단점이라, 내장 기능으로 옮기면 자동화된다.

## `app/sitemap.ts` 구현

기존 `public/sitemap.xml`을 지우고 `app/sitemap.ts`를 만든다.

```typescript
import type { MetadataRoute } from 'next'

// 정적 export(output: 'export') 환경에서 빌드 시 파일로 구워지도록 강제
export const dynamic = 'force-static'

async function getBlogPosts() {
  // 예: const res = await fetch('https://api.example.com/posts')
  return [
    { id: '1', updatedAt: '2026-06-16' },
    { id: '2', updatedAt: '2026-06-15' },
  ]
}

export default async function sitemap(): Promise<MetadataRoute.Sitemap> {
  const baseUrl = 'https://yoursite.com'

  const staticRoutes = [
    { url: baseUrl, lastModified: new Date(), changeFrequency: 'daily' as const, priority: 1.0 },
    { url: `${baseUrl}/about`, lastModified: new Date(), changeFrequency: 'monthly' as const, priority: 0.8 },
  ]

  const posts = await getBlogPosts()
  const dynamicRoutes = posts.map((post) => ({
    url: `${baseUrl}/blog/${post.id}`,
    lastModified: new Date(post.updatedAt),
    changeFrequency: 'weekly' as const,
    priority: 0.6,
  }))

  return [...staticRoutes, ...dynamicRoutes]
}
```

## 핵심 — `export const dynamic = 'force-static'`

정적 배포(`output: 'export'`) 환경에서 사이트맵을 **빌드 시 실제 XML 파일로 구워내도록** 강제하는 옵션. 이게 있어야 빌드 때 외부 데이터를 호출한 뒤 `out/sitemap.xml`로 생성된다.

## 동작 확인

- [ ] **개발 모드**: `npm run dev` → `http://localhost:3000/sitemap.xml` 접속 시 실시간 변환된 XML 확인
- [ ] **정적 배포**: `npm run build` → `out/sitemap.xml`에 최종 XML 생성

## 관련 노트

- [[sitemap.xml]] — 이 기능이 생성하는 파일의 개념과 표준 구조
