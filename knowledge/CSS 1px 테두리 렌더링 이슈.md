---
tags:
  - css
  - browser
  - rendering
  - windows
---
물리적 디스플레이는 정수 단위 픽셀로 구성되지만, CSS 계산 결과는 종종 소수점 값이 나온다. 브라우저가 이를 처리하는 방식의 차이에서 ==서브 픽셀 렌더링 문제==가 발생하며, 특히 **1px 테두리가 완전히 사라지는** 현상으로 나타난다.

## 주요 발생 상황

**1. 레이아웃 반올림 불일치**
```css
/* 컨테이너 999px, 자식 3개에 33.33%씩 → 333.3px */
.item { width: 33.33%; }
```
브라우저마다 333px 또는 334px으로 반올림 기준이 달라 **1px 갭**이나 overflow가 생긴다.

**2. 소수점 좌표 흐림(blur)**
```css
.element {
  position: absolute;
  left: 10.5px; /* 안티앨리어싱으로 번짐 */
}
```

**3. `translate(-50%, -50%)` 중앙 정렬**
요소의 width/height가 홀수이면 `-50%` 결과가 `.5px`이 되어 텍스트·이미지가 흐릿해진다.

**4. 애니메이션 중 깜빡임(jitter)**
transition/animation이 소수점 값을 지나칠 때 렌더 레이어가 픽셀 그리드에서 이탈하며 떨림 발생.

## OS별 픽셀 스내핑 방식

소수점 픽셀은 물리적으로 켤 수 없으므로 반드시 정수로 변환된다.

| OS | 방식 | 결과 |
|---|---|---|
| Windows | **픽셀 스내핑** — 기준 미만이면 버림(0) | 선이 완전히 사라짐 |
| macOS / iOS | **안티앨리어싱** — 소수점을 흐릿하게 채움 | 선은 유지되나 흐릿함 |

**Windows DPI 배율 환경**: 디스플레이 배율 125%, 150% 설정 시 `window.devicePixelRatio`가 1.25, 1.5 등 소수값이 된다. CSS 1px × DPR 1.25 = **1.25 물리 픽셀** → 브라우저가 0으로 내림하면 미표시.

## 우측 테두리만 끊기는 이유

레이아웃을 왼쪽→오른쪽 순서로 계산할 때, 앞 요소들의 소수점 오차가 우측으로 갈수록 **누적**된다. 마지막 우측 경계선에서 누적 오차가 터지며 그리드 범위를 벗어나거나 버림 처리되어 오른쪽 선만 끊긴다.

## 브라우저별 처리 차이

| 브라우저 | 처리 방식 |
|---|---|
| Chrome/Edge | 레이아웃은 부동소수 유지, 페인트 시 반올림 |
| Firefox | 서브 픽셀 레이아웃을 더 적극적으로 유지 |
| Safari | 1px 보더 등에서 독자적 렌더링 |

---

## 해결 방법

### 1px 보더 소멸 방지

**box-shadow로 대체 (가장 추천)**
`border`의 소수점은 버림되지만 `box-shadow`는 훨씬 정밀하게 계산된다.

```css
/* 사방 전체 문제일 때 — inset 그림자로 테두리 구현 */
.element {
  box-shadow: inset 0 0 0 1px #e0e0e0;
}

/* 한쪽 방향만 문제일 때 — border + shadow 혼합 */
.element-right-issue {
  border: 1px solid #e0e0e0;
  border-right: none;
  box-shadow: 1px 0 0 0 #e0e0e0;
}
```

**`border-width: thin` 키워드**
브라우저가 "아무리 축소되어도 최소 1 물리 픽셀은 보장"하도록 강제한다.
```css
.element {
  border: thin solid #e0e0e0;
}
```

**`calc()`로 미세 오차 보정 (Flex 레이아웃)**
```css
.flex-child {
  width: calc(33.33% - 0.5px);
}
```

> [!warning] `outline` 사용 시 주의
> `border` 대신 `outline: 1px solid`도 서브 픽셀 안전하지만, 레이아웃 흐름에 영향을 주지 않으므로 의도치 않은 겹침이 생길 수 있다.

### 위치 흐림 방지 — GPU 레이어 승격

```css
.element {
  transform: translateZ(0);
  /* 또는 */
  will-change: transform;
}
```

> [!warning] 남용 주의 — GPU 메모리 소비. 실제 애니메이션이 있는 요소에만 적용할 것.

### 중앙 정렬 흐림 방지

```css
/* flexbox 우선 */
.parent {
  display: flex;
  align-items: center;
  justify-content: center;
}
```
`translate(-50%, -50%)` 방식을 써야 한다면 요소의 width/height를 **짝수값**으로 맞춘다.

### 레이아웃 1px 갭 방지

```css
/* 퍼센트 직접 연산 대신 grid fr 단위 사용 */
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

### 고밀도 디스플레이(레티나) 1px 보더

```css
@media (-webkit-min-device-pixel-ratio: 2) {
  .element::after {
    content: '';
    display: block;
    transform: scaleY(0.5);
    border-top: 1px solid #ccc;
  }
}
```

## 핵심 원칙

1. 1px 테두리는 `border` 대신 `box-shadow: inset 0 0 0 1px` 사용
2. 레이아웃엔 `flex` / `grid` — 퍼센트 직접 연산 최소화
3. 애니메이션은 `transform` / `opacity`만 (GPU 합성 레이어 활용)
4. 중앙 정렬은 flexbox 우선, `translate` 쓸 경우 짝수 크기 보장
5. `translateZ(0)` / `will-change`는 꼭 필요한 요소에만

## 관련 노트

- [[qshop cs/Windows 1px 테두리 미표시 - 상품 슬라이드 블록]]
