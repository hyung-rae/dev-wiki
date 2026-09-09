---
tags:
  - nextjs
  - router
---
==Router는 페이지 이동과 관련된 기능을 담고 있는 객체==다. Next.js는 파일 구조가 곧 경로이므로, 이동은 이 객체의 메서드로 처리한다.

| 멤버 | 역할 |
| --- | --- |
| `Router.pathname` | 현재 위치 주소 (파일 경로 형태) |
| `Router.asPath` | 현재 위치 주소 (**실제 표시되는** 주소) |
| `Router.push('/')` | 다른 페이지로 이동 |
| `Router.replace('/')` | **현재 페이지를 기록에서 지우고** 이동 |
| `Router.back()` | 뒤로 가기 |
| `Router.reload()` | 새로고침 |

```javascript
import Router from 'next/router';

export default function Routing() {
  const handleClickPush = () => {
    Router.push('/');
  };

  const handleClickReplace = () => {
    Router.replace('/');
  };

  return (
    <>
      <button onClick={handleClickPush}>다른 페이지로 이동</button>
      <button onClick={handleClickReplace}>현재 페이지 삭제 후 이동</button>
    </>
  );
}
```

> [!tip]
> `push`와 `replace`의 차이는 **히스토리에 남느냐**다. 로그인 처리 직후처럼 뒤로 가기로 돌아오면 안 되는 화면에는 `replace`를 쓴다.

## pathname vs asPath
동적 라우팅에서 갈린다. `/board/[id]` 페이지를 `/board/3`으로 접속하면 `pathname`은 `/board/[id]`, `asPath`는 `/board/3`이다. **화면에 보이는 실제 주소로 비교**해야 할 땐 `asPath`를 쓴다.

## 관련 노트
- [[Next.js 동적 라우팅]] — 경로에 변수를 담는 방법
- [[props.children과 레이아웃 컴포넌트]] — `asPath`로 레이아웃을 조건부 렌더링
- [[Next.js와 SEO]]
