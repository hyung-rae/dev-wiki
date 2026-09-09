---
tags:
  - react
  - lifecycle
  - componentDidMount
---
클래스 컴포넌트는 **화면에 그려지고 → 갱신되고 → 사라지는** 각 시점에 끼어들 수 있는 메서드를 제공한다.

| 메서드 | 실행 시점 |
| --- | --- |
| `render` | 화면을 그릴 때 |
| `componentDidMount` | 화면을 **그리고 난 후** (최초 1회) |
| `componentDidUpdate` | 그린 뒤 **변경되었을 때** |
| `componentWillUnmount` | 화면이 **사라질 때** (페이지 이동 등) |

```javascript
export default class MyLifecyclePage extends Component {
  inputRef = createRef<HTMLInputElement>(null);
  state = { count: 0 };

  componentDidMount() {
    console.log("마운트됨");
    this.inputRef.current?.focus();
  }

  componentDidUpdate() {
    console.log("수정됨");
  }

  componentWillUnmount() {
    console.log("끝났음");
  }

  render() {
    return (
      <>
        <input type="text" ref={this.inputRef} />
        <div>현재카운트 : {this.state.count}</div>
      </>
    );
  }
}
```

> [!info]
> `componentDidMount`가 **그리고 난 후**에 실행된다는 점이 중요하다. DOM에 접근하거나 API를 호출하는 코드는 여기에 둬야 한다. 함수형 컴포넌트에서는 `useEffect`가 이 역할을 전부 대신한다.

## 관련 노트
- [[React 클래스 컴포넌트]] — 생명주기 메서드를 갖는 형태
- [[useEffect와 의존성 배열]] — 함수형에서의 대응
- [[React Ref와 createRef]] — 마운트 이후 DOM에 접근하는 수단
- [[React]]
