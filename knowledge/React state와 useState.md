---
tags:
  - react
  - state
  - useState
---
==state는 컴포넌트가 쓰는 변수==다. 일반 변수와 달리 **값이 바뀌면 화면이 다시 그려진다.** 그래서 만드는 법과 바꾸는 법이 따로 있다.

| 이름 | 역할 |
| --- | --- |
| `state` | 컴포넌트에서 사용하는 변수 |
| `useState` | 그 변수를 **만드는** 기능 |
| `setState` | 그 변수를 **바꾸는** 기능 |

## JavaScript 변수와 대비
```javascript
// JavaScript
let classmate = "철수";
classmate = "영희";

// React 컴포넌트
const [classmate, setClassmate] = useState("철수");
setClassmate("영희");
```

`const [변수명, 변수바꾸는기능] = useState(초기값)` 형태의 **배열 구조 분해**다. 변수 자체는 `const`이고, 값 변경은 오직 setter를 통해서만 이뤄진다.

> [!warning]
> `classmate = "영희"`처럼 **직접 대입하면 화면이 갱신되지 않는다.** React는 setter 호출을 통해서만 리렌더링이 필요하다는 것을 안다.

## 관련 노트
- [[setState의 prev - 함수형 업데이트]] — setter를 연속 호출할 때 생기는 문제
- [[React State 끌어올리기]] — state를 여러 컴포넌트가 공유하는 방법
- [[React 컴포넌트 - 클래스형과 함수형]]
- [[React]]
