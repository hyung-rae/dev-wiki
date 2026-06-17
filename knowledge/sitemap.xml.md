---
tags:
  - sitemap
  - seo
---

`sitemap.xml`은 웹사이트의 **모든 페이지 목록을 담은 XML 파일(웹사이트 지도)**이다. 검색엔진 크롤러에게 사이트 구조를 알려 페이지가 빠르고 정확하게 ==인덱싱==되도록 돕는 **SEO 필수 요소**다.

## 봇이 찾는 경로

크롤러(구글·네이버 등)는 사이트 방문 시 약속된 기본 경로인 **루트(`https://도메인/sitemap.xml`)**를 가장 먼저 찾아 읽는다. 그래서 사이트맵은 반드시 최상위 루트에 위치해야 한다.

## 표준 구조

큰 틀(`urlset`) 안에 각 페이지 정보(`url`)가 카드처럼 들어간다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://www.example.com/</loc>
    <lastmod>2026-06-16</lastmod>
    <changefreq>daily</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

| 태그 | 의미 |
| --- | --- |
| `loc` | 페이지 URL (필수) |
| `lastmod` | 마지막 수정일 |
| `changefreq` | 변경 빈도 힌트 (`daily`·`weekly`·`monthly` 등) |
| `priority` | 사이트 내 상대 중요도 (0.0~1.0) |

## 관련 노트

- [[Next.js 사이트맵 자동 생성]] — 이 파일을 프레임워크 내장 기능으로 자동 생성하는 방법
