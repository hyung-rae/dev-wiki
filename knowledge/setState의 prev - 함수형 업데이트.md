---
tags:
  - react
  - state
  - prev
  - troubleshooting
---
`setState`는 즉시 반영되지 않고 ==임시 저장 공간에 모아두었다가 한 번에 처리==된다. 이 특성 때문에 setter를 연속 호출하면 직관과 다른 결과가 나온다.

## 값을 직접 넣으면 마지막 한 번만 반영된다
```javascript
const [count, setCount] = useState(0);

const onClickPlus = () => {
  setCount(count + 1);
  setCount(count + 1);
  setCount(count + 1);
  setCount(count + 1);
};
// 결과: count는 1
```

네 번 모두 **같은 시점의 `count`(=0)를 읽어서** `0 + 1`을 넣기 때문이다.

## prev를 쓰면 임시 저장 공간의 값을 이어받는다
```javascript
const onClickPlus = () => {
  setCount((prev) => prev + 1);
  setCount((prev) => prev + 1);
  setCount((prev) => prev + 1);
  setCount((prev) => prev + 1);
  setCount((prev) => prev + 1);
};
// 결과: 한 번 실행에 5 증가
```

**`prev`는 임시 저장 공간에 쌓여 있는 최신 값**이다. 함수를 넘기면 React가 그 값을 인자로 넣어준다.

> [!tip]
> **이전 값에 의존하는 갱신은 무조건 `prev`를 쓴다.** 토글처럼 단순한 경우에도 예상 못 한 버그를 막아준다.
> ```javascript
> const showModal = () => {
>   setIsModalVisible((prev) => !prev);
> };
> ```

## 관련 노트
- [[React state와 useState]] — setter의 기본 사용법
- [[React 클래스 컴포넌트]] — `this.setState`에서도 같은 규칙이 적용된다
- [[React]]
