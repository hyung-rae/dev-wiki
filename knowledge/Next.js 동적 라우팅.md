---
tags:
  - nextjs
  - dynamic-routing
---
Next.js의 라우팅은 **폴더 구조가 곧 URL**이고, 해당 폴더의 `index.js`가 실행된다. 이때 경로가 고정인지 아닌지에 따라 두 가지로 나뉜다.

| | static routing | dynamic routing |
| --- | --- | --- |
| 성격 | 항상 변하지 않는 페이지 | 요청 값에 따라 내용이 변하는 페이지 |
| 예시 | 로그인, 회원가입 | 목록에서 선택한 게시글 상세 |
| 폴더명 | 일반 이름 | **`[변수명]`** |

## 폴더명을 변수로 만든다
```text
pages/
└── 05-02-product-read/
    └── [productId]/
        └── index.js
```

대괄호로 감싼 폴더명이 **URL 세그먼트를 받는 변수**가 된다.

```javascript
// 보내는 쪽 — 값을 경로에 실어 이동
router.push(`/05-02-product-read/${result.data.createProduct._id}`);
```

```javascript
// 받는 쪽 — 폴더명과 같은 키로 꺼낸다
const data = router.query.productId;
```

> [!warning]
> `router.query`는 **첫 렌더링에서 비어 있을 수 있다.** 이 값으로 바로 API를 호출하면 `undefined`가 넘어가므로, 값이 채워졌는지 확인하고 써야 한다.

## 관련 노트
- [[Next.js Router 객체]] — `push`와 `query`를 제공하는 객체
- [[Next.js와 SEO]]
