---
tags:
  - react
  - useEffect
  - dependency-array
  - react-hook
---
`useEffect`는 ==컴포넌트가 그려진 이후에 실행되는 함수==다. **언제 다시 실행할지는 두 번째 인자인 의존성 배열이 결정한다.**

| 두 번째 인자 | 실행 시점 |
| --- | --- |
| `[]` (빈 배열) | **최초 한 번만** |
| 생략 (인자 없음) | 최초 1회 + **무언가 변경될 때마다** |
| `[count]` | 최초 1회 + **`count`가 바뀔 때마다** |

```javascript
useEffect(() => {
  console.log("최초 한 번 실행됨 — 의존성 배열이 비어있으니까");
}, []);

useEffect(() => {
  console.log("무언가 변경될 때마다 실행됨 — 배열 자체를 안 넣었으니까");
});

useEffect(() => {
  console.log("count가 변경되면 재실행 — 배열에 count를 넣었으니까");
}, [count]);
```

## 흔한 함정 두 가지
```javascript
// 1. 불필요한 리렌더링 — state를 재설정해서 렌더링이 두 번 일어난다
useEffect(() => {
  setCount(100);
}, []);

// 2. 무한 루프 — count를 바꾸는데 의존성에 count가 들어있다
useEffect(() => {
  setCount((prev) => prev + 1);
}, [count]);
```

> [!warning]
> **의존성 배열에 든 값을 effect 안에서 바꾸면 무한 렌더링에 빠진다.** effect 안에서 `setState`를 호출해야 한다면 의존성을 다시 따져봐야 한다.

## API 호출 — 최초 1회 패턴
서버에서 한 번만 데이터를 받아오는 경우가 `[]`의 대표적 용도다.

```javascript
const fetchWeather = async () => {
  const result = await axios.get(
    `https://api.openweathermap.org/data/2.5/weather?q=Seoul,kr&appid=${process.env.REACT_APP_API_KEY}`
  );

  setWeatherInfo({
    cityName: result.data.name,
    humidity: result.data.main.humidity,
    temp: result.data.main.temp,
  });
};

useEffect(() => {
  fetchWeather();
}, []);
```

## 관련 노트
- [[React 컴포넌트 생명주기]] — `useEffect`가 대신하는 클래스형 메서드들
- [[React state와 useState]] — 의존성 배열에 들어가는 값
- [[setState의 prev - 함수형 업데이트]]
- [[React]]
