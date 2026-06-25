---
tags:
  - knowledge
  - css
  - flexbox
  - baseline
---

Flexbox `align-items`에서 `flex-start`는 **요소(박스)의 윗면**을, `baseline`은 **박스 안 글자의 기준선(아랫선)**을 정렬 기준으로 삼는다.

- **`flex-start` (박스 기준)**: 요소의 가장 윗면을 컨테이너 천장에 맞춘다. 안의 글자 크기가 다르면 글자의 높낮이가 들쭉날쭉해진다.
- **`baseline` (텍스트 기준)**: 박스 윗면은 삐뚤빼뚤해지더라도, 글자들의 ==베이스라인(기준선)==을 한 줄로 맞춘다.

## 비교

| 속성값 | 정렬 기준 | 주로 쓰는 상황 |
| --- | --- | --- |
| `flex-start` | 박스(요소)의 **윗면** | 박스 상단 라인을 칼같이 맞춰야 할 때 |
| `baseline` | 박스 안 **글자의 바닥선** | 크기가 다른 **텍스트**를 자연스럽게 한 줄로 이을 때 |

> [!tip] baseline은 사실상 텍스트 전용
> 박스 안에 글자가 없고 이미지나 빈 박스만 있으면 `baseline`은 큰 의미가 없다.
> - **가격 표시**: `15,000`(큰 글씨) + `원`(작은 글씨)을 나란히
> - **더보기 버튼**: `공지사항 제목`(큰 글씨) + `더보기 >`(작은 글씨)를 나란히

## 코드 예시

```html
<div style="display: flex; align-items: baseline;">
  <span style="font-size: 32px;">15,000</span>
  <span style="font-size: 14px;">원</span>
</div>
```

![[251f63d9-be75-4b7c-bcad-8435200d4f72.jpeg]]