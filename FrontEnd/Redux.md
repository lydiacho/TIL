`라이브러리`

별도의 파일을 하나 만들어서 내가 원하는 **state들을 다 모아둔다.**

그리고 rprops drilling 없이 곧바로 여러 파일에서 사용한다.

- 설치해야할 라이브러리
  - `import { Provider } from 'react-redux';`
  - `import { createStore } from 'redux';`

### 기본적인 세팅

- `reducer` 함수
  - 인수 : state, action
  - 반환값 : state

> 핵심 : **`reducer 함수`** 정의, `**createStore`메소드** 사용, `**Provider**`로 감싸주기 \*\***

```jsx
// index.js

import { Provider } from 'react-redux';
import { createStore } from redux;

// 원하는 state를 정의한다.
const 상태명 = 초기값;

function reducer(state = 상태명, action) {
	return state
}

let store = createStore(reducer)

// 반환해주는 html 내부에서 <App/>을 Provider로 감싸준다.
<Provider store={store}>
	<App />
</Provider>
```

### 기본적인 사용법

> 핵심 : `**useSelector` 메소드\*\*를 사용한다.

```jsx
import { useSelector } from 'react-redux'

function 컴포넌트() {
	const 변수명 = useSelector( (state) => state );

	return (
	// 여기서 알아서 state 사용 -> {state}
	);
}

export default 컴포넌트;
```

### Redux의 state 관리

- state의 값을 **변경**하고 싶을 때
- 별도의 파일에 state만 만들어놓고 해당 값을 각기 다른 파일에서 자유롭게 수정할 때, 오류가 발생하면 추적하기 매우 힘들다.
- Redux를 사용하면 별도의 파일에서 **`state 값을 수정할 방법`**까지 사전에 정의를 해놓고, 이를 가져다가 쓰는 것이기 때문에, **state update에 대한 추적이 용이**해진다.
- 즉 별도의 파일에서 API를 짜는 것과 같다.
- 컴포넌트들은 state를 직접 수정하지 못하고, 별도의 관리 파일에 **수정을 요청**해야만 하도록 제한하여 오류를 추적, 관리할 수 있다.

이것이 오류 추적이 어려운 큰 규모의 프로젝트의 경우, Redux를 사용해야 하는 이유이다.

### action 정의 방법

- 즉 state 값 수정 방법 정의하는 법

> 핵심 : `**action의 type`별 분기\*\*를 처리해준다.

```jsx
// index.js

// ...

function reducer(state = 상태명, action) {
  if (action.type === "증가") {
    state++;
    return state;
  } else if (action.type === "감소") {
    state--;
    return state;
  } else {
    return state;
  }
}

// ...
```

### action 사용법

- 컴포넌트가 별도의 파일한테 state 수정을 요청하는 법

> 핵심 : `**useDispatch` 메소드\*\*를 사용한다

```jsx
// ...

function 컴포넌트명() {
  const 변수명 = useSelector((state) => state);
  const dispatch = useDispatch();

  return (
    <div>
      {/* 여기서 dispatch를 자유롭게 사용한다. 아래는 예시 */}
      <button
        onClick={() => {
          dispatch({ type: "증가" });
        }}
      >
        {" "}
        버튼명{" "}
      </button>
    </div>
  );
}

export default 컴포넌트명;
```
