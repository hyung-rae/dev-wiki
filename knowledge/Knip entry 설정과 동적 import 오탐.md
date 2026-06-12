---
tags:
  - knip
  - entry
  - dynamic-import
  - dead-code
  - troubleshooting
---
Knip 설정의 `entry`는 ==도달성(reachability) 분석의 출발점 파일 목록 배열==이다. Knip은 이 entry 파일들을 루트로 삼아 `import` 사슬을 타고 그래프를 그리고, **어디에도 닿지 않는 파일을 "미사용(unused)"으로 분류**한다.

```
entry 파일 ──import──▶ A ──import──▶ B ──▶ C
                          └──import──▶ D
→ entry에서 닿는 A·B·C·D = 사용 중(보호됨)
→ 안 닿는 파일 = 미사용 = 삭제 후보
```

> [!info] entry에 등록된 파일과 거기서 import로 연결된 모든 파일은 **절대 미사용으로 분류되지 않는다.** entry는 "import 당하지 않아도 실행되는 코드"를 Knip에게 알려주는 장치다.

## 왜 entry가 따로 필요한가
대부분의 파일은 누군가 `import`해서 쓰이지만, **아무도 import하지 않지만 실행되는** 파일들이 있다 — 이들은 import 그래프 상 고아지만 실제 시작점이다.
- **페이지/라우트** — `pages/**/index.js`는 코드가 아니라 라우터가 URL로 실행
- **config** — `next.config.js`, `sentry.*.config.ts`
- **스크립트** — `scripts/*.mjs` (CLI 직접 실행)
- **서버 엔트리** — `server/**`

> [!tip] `entry`가 "출발점"이라면 `project`는 "분석 대상 전체 범위"다. project에 있지만 entry에서 안 닿으면 미사용으로 잡힌다.

## Next.js는 상당수 자동 감지
Knip의 Next 플러그인이 `next.config`·`pages/**`·`app/**`·`server`·`instrumentation`을 **자동으로 entry 취급**한다. 중복으로 적으면 `Remove redundant entry pattern` 경고가 뜨므로, 자동 감지 안 되는 것만 추가한다.

## 동적 import 오탐 — entry가 필요한 또 하나의 핵심 케이스
Knip은 ==`dynamic(() => import())`(next/dynamic) 같은 동적 import를 추적하지 못해, 살아있는 코드를 "미사용 파일"로 오판==한다. 모르고 삭제하면 런타임에 해당 기능이 깨진다.

### 왜 오탐하는가
Knip의 도달성 분석은 import 경로가 **정적으로 코드에 박혀 있을 때만** 그래프 엣지로 연결한다. `next/dynamic`은 import가 **함수 안에 감싸진 런타임 호출**이라 정적 분석에서 엣지로 잡히지 않는다.

```js
// 이 파일 자체는 살아있는 코드인데도...
const Editor = dynamic(
  () => import('@/components/Editor/Editor'),  // ← Knip이 이 엣지를 못 봄
  { ssr: false },
)
```
→ `Editor`를 import하는 정적 구문이 0건으로 보여 **미사용으로 분류** → 삭제 후보로 올라온다.

> [!danger] 빌드는 통과할 수 있어 더 위험하다. 번들에서 빠진 게 정상처럼 보이고, 실제 사용자가 그 화면에 진입할 때 비로소 깨진다. Knip을 삭제 후 재실행해도 동적 import는 unresolved로도 안 잡혀 못 거른다.

### 교정 — 동적 대상을 entry로 등록
못 따라가는 동적 import의 **대상 파일 자체를 entry로 등록**한다. 그러면 Knip이 그 파일을 새 출발점으로 삼아 아래 정적 사슬을 전부 "도달 가능"으로 복구한다.

1. 코드베이스에서 `dynamic(() => import(...))` / `dynamic(import(...))` 패턴 전부 수집
2. 각 import 경로의 alias를 **프로젝트의 alias 규칙으로 실제 경로 resolve** (예: `@/`가 `src/`나 루트 중 어디를 가리키는지)
3. resolve된 파일들을 `knip.json`의 `entry`에 추가

> [!tip] 파일 1~2개의 일회성 예외라면 `// @knipignore` 주석으로도 처리 가능하다. 동적 대상이 다수면 entry 등록이 그래프 전체를 복구하므로 더 견고하다.

### 그래도 entry만 믿지 않는다 — 삭제 전 3중 게이트
모든 동적 패턴을 100% 수집했다는 보장이 없으므로 삭제 직전 한 번 더 검증한다.
1. Knip 도달성 분석 (정적)
2. 삭제 대상을 import하는 reachable 파일이 **정적 `from`·동적 `import()`·`require` 통틀어 0건**인지 grep 직접 확인
3. 실제 빌드 통과 (`Module not found` 0건)

## 관련 노트
- [[Knip - 데드 코드·의존성 청소 도구]] — entry 그래프 추적을 수행하는 도구 본체이자, 그 한계가 동적 import 오탐을 낳음
