---
layout: cover
background: none
drawings:
    presenterOnly: true
theme: seriph
---

# React 중앙상태관리

---

# React 상태관리

<div style="display: flex; align-items: center; justify-content: space-between;">
    <img src="https://i.postimg.cc/SRPqRkFR/page-component.jpg" style="width: 40%" />
    ===>
    <v-click>
        <img src="https://i.postimg.cc/j2b3h1Hc/props.jpg" style="width: 40%;">
    </v-click>
    <v-click>
        <img src="https://i.postimg.cc/TP9krkyr/state.gif" style="width: 40%; position: absolute; left: 55%">
    </v-click>
</div>

---

# 중앙상태관리

### 왜 써야 하는가?

1. Props 문법 줄일 수 있음
2. 상태를 전역적으로 관리할 수 있음
3. 유지보수가 쉬움

---

# Context API는 어떤가요?

1. Props 문법 줄일 수 있음
2. React에 내장되어 있어서 별도의 라이브러리 설치가 필요 없음

-   간단 예시

```js {all} {maxHeight: '300px'}
// Context 생성
import { Dispatch, PropsWithChildren, createContext, useContext, useState } from "react";

interface SettingContext {
    theme: [string | undefined, Dispatch<string | undefined>];
    locale: [string | undefined, Dispatch<string | undefined>];
}

const settingContext = createContext<SettingContext>( {} as SettingContext );

export function SystemMonitoringProvider( props: PropsWithChildren )
{
    const theme = useState<string | undefined>( "dark" );
    const locale = useState<string | undefined>( "kr" );

    return <settingContext.Provider
        value={{
            theme,
            locale,
        }}
    >
        {props.children}
    </settingContext.Provider>;
}

export function useSettingContext( )
{
    const context = useContext( settingContext );

    return {
        context,
    };
}

// Provider로 감싸기
import React from 'react';
import { SettingProvider } from './setting.context';

const App: React.FC = () => {
  return (
    <SettingProvider>
      <div className="app">
        <h1>React Context API 예시</h1>
        <ThemeSelector />
        <LocaleSelector />
      </div>
    </SettingProvider>
  );
};

export default App;

// Context 사용
import React from 'react';
import { useSettingContext } from './setting.context';

export default fucntion ThemeSelector() {
  const { theme } = useSettingContext();

  return (
    <div>
      <span>테마</span>
      <Select option={ThemeOption} value={theme} />
    </div>
  );
};
```

---

# Context API 주의사항

-   특정 Context에 의존하기 때문에 컴포넌트간 결합도 증가 => 재사용 어려움
-   상태 변경 시 Context를 구독하고 있는 모든 컴포넌트가 리렌더링 됨

  <img src="https://i.postimg.cc/W30yRVSg/context.jpg" style="width: 40%;">

---

# Context API 언제 써야하나?

### React 공식 문서

-   전역적 ( global ) 데이터를 공유할 때
    > context는 React 컴포넌트 트리 안에서 전역적(global)이라고 볼 수 있는 데이터를 공유할 수 있도록 고안된 방법입니다.<br/>
    > 그러한 데이터로는 현재 로그인한 유저, 테마, 선호하는 언어 등이 있습니다.

<br/>

### 결론

-   Context는 전역적으로 데이터를 공유하는 API
-   반복적이고 복잡한 업데이트에 사용할 경우 비효율적일 수 있음

**낮은 빈도로 업데이트가 일어나는 데이터를 공유할 때 사용하는 것이 좋음**

---

# Redux 를 더 많이 쓰던데?

### 초기 React

-   전역 상태를 관리하기 위한 라이브러리 없음
-   Context API 또한 16.3 이 후 추가 된 API
-   Prop Drilling이 React의 유지보수를 어렵게 만듬
-   예전 웹 앱은 MVC 패턴으로 구현되었음

---

# MVC 패턴

<img src="https://i.postimg.cc/X7H5jnLD/MVC.jpg" style="width: 40%">

-   웹 앱의 규모 증가 => 다양한 Model, View가 생김
-   데이터 변경 시 해당 데이터를 사용하는 **모든 곳의 코드를 수정해야 함**

---

# Flux 패턴

<img src="https://i.postimg.cc/50JwTn9B/flux.jpg" style="width: 40%">

-   MVC 패턴의 단점을 보완하기 위해 Facebook에서 만든 패턴
-   단방향 데이터 흐름 아키텍처 패턴
-   상태 관리를 단순화하고 예측 가능한 변화를 제공

---

# Redux는 Flux 패턴을 구현한 라이브러리

-   금방 상태관리 라이브러리의 대세로
-   React용이 아닌 Vanilla JS용으로 만들어짐
-   상태를 안정적으로 유지하기 위해 Flux 패턴에 맞게 많은 반복적인 코드 작성 필요
<p style="fontWeight: bold">Redux Boilerplate</p>

---

# Redux Boilerplate

### Action

-   상태를 변화시키기 위해 발생시키는 이벤트

### Reducer

-   상태가 변화하는 로직을 담당

### Dispatch

-   Action을 발생시키는 함수

### Store

-   상태를 담고있는 객체

---

# Redux Boilerplate 예시

```js {all} {maxHeight: '400px'}
// Action 정의
export const INCREMENT = "INCREMENT";
export const DECREMENT = "DECREMENT";

export const increment = () => ({
    type: INCREMENT,
});

export const decrement = () => ({
    type: DECREMENT,
});

// Reducer 를 작성하여 상태 변화 로직 구현
import { INCREMENT, DECREMENT } from "./actions";

const initialState = {
    count: 0,
};

const counterReducer = (state = initialState, action) => {
    switch (action.type) {
        case INCREMENT:
            return {
                ...state,
                count: state.count + 1,
            };
        case DECREMENT:
            return {
                ...state,
                count: state.count - 1,
            };
        default:
            return state;
    }
};

export default counterReducer;

// Reducer를 합치고 Store를 생성
import { createStore } from "redux";
import counterReducer from "./reducers";

const store = createStore(counterReducer);

export default store;

// Provider를 통해 App에 Store를 연결
import React from "react";
import { Provider } from "react-redux";
import store from "./store";
import Counter from "./Counter";

const App = () => {
  return (
    <Provider store={store}>
      <div className="app">
        <h1>Redux 카운터 앱</h1>
        <Counter />
      </div>
    </Provider>
  );
};

// 위 과정을 통해 Redux를 사용할 수 있게 됨
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { increment, decrement } from "./actions";

const Counter = () => {
  const count = useSelector((state) => state.count); // store의 state를 가져옴
  const dispatch = useDispatch(); // dispatch를 이용하여 action을 발생시킴

  return (
    <div>
      <h1>카운터: {count}</h1>
      <button onClick={() => dispatch(increment())}>증가</button>
      <button onClick={() => dispatch(decrement())}>감소</button>
    </div>
  );
};
```

---

# React-Redux v6의 Context API 도입과 성능 최적화

-   Redux는 React 16.3에서 새로 도입된 createContext API를 도입
-   Redux Store State를 Context API를 통해 전파하였으나, 이는 v5 대비 성능이 떨어짐
-   Redux v7 부터는 Store의 상태 변경 시에만 Context API를 사용하는 방식으로 변경
-   Store와 connect 시 React.memo를 사용하여 성능 최적화 <br>
    [참고 React-Redux 7.0 History](https://blog.isquaredsoftware.com/2018/11/react-redux-history-implementation/#v7-0)

---

# Redux의 단점

-   상태 관리를 위한 비용이 많이 듦
-   반응형 업데이트, 비동기 처리 등을 위해 라이브러리를 추가로 사용해야 함
    -   redux-thunk
    -   redux-saga
    -   redux-toolkit
        <br/><br/>

### 결론

**러닝커브가 높고, 비용이 많이 들어서 Redux를 사용하기 위해 많은 시간을 투자해야 함**

---

# Recoil은 어떻게 다른가요?

<img src="https://i.postimg.cc/NM7SZYfS/recoil.png" style=""><br>

-   React를 구현한 Facebook에서 만든 상태 관리 라이브러리
-   **배우기 쉽다**
-   hook과 동일한 사용방식

> React v18부터 활발히 개발중에 있는 Concurrent Mode와 개발 방향성이 같습니다. <br>
> Recoil에서 Transition을 지원하는 기능을 개발하여 무거운 컴포넌트의 경우 **상태 업데이트 중 상위 Suspense를 호출**하는 기능을 개발중에 있습니다.

---

# Recoil 시작하기

-   앱의 최상위를 RecoilRoot로 감싸고, atom 단위로 선언하여 사용

```js
import React from "react";
import ReactDOM from "react-dom";
import { RecoilRoot } from "recoil";
import App from "./App";

export default function App() {
    return (
        <RecoilRoot>
            <AppMain />
        </RecoilRoot>
    );
}

createRoot(app).render(<App />);
```

---

# Atoms

<img src="https://i.postimg.cc/J0Q1ZtYN/atom.png" style="width: 40%">

-   상태의 단위. Atom을 통해 상태를 정의하고, 업데이트하거나 구독할 수 있음
-   Atom이 업데이트되면 구독하고 있는 컴포넌트가 리렌더링 됨
-   고유한 키와 초기값을 이용하여 정의
-   Atom Hook
    -   **useRecoilState** : Read/Write
    -   **useRecoilValue** : Read Only
    -   **useSetRecoilState** : Write Only

---

# Atom 사용 예시

```js
import { atom } from "recoil";

export const counterState = atom({
    key: "counterState",
    default: 0,
});
```

```js {all} {maxHeight: '300px'}
import React from "react";
import { useRecoilState } from "recoil";
import { counterState } from "./atoms";

export default function Counter() {
    const [count, setCount] = useRecoilState(counterState);

    const handleIncrement = () => {
        setCount((prevCount) => prevCount + 1);
    };

    const handleDecrement = () => {
        setCount((prevCount) => prevCount - 1);
    };

    return (
        <div>
            <h1>카운터: {count}</h1>
            <button onClick={handleIncrement}>증가</button>
            <button onClick={handleDecrement}>감소</button>
        </div>
    );
}
```

---

# atom with TypeScript

Recoil은 Typescript를 지원함

```ts
import { atom } from "recoil";
import { User } from "./types";

interface User {
    name: string;
    age: number;
}

export const userAtom = atom<User>({
    key: "userAtom",
    default: {
        name: "",
        age: 0,
    },
});
```

---

# selector

상태에서 파생된 데이터를 정의

-   하나 이상의 atom을 읽어서 계산된 값을 반환하는 상태를 정의할 수 있음
-   구현한 구조에 따라 반환되는 객체가 다름

    -   get 함수만 구현 : RecoilValueReadOnly
    -   set 함수도 구현 : RecoilState

---

# 읽기 전용 selector

의존하는 상태가 변경될 때만 재계산하여 리렌더링 수행

```js
import { atom, selector } from "recoil";

const number1State = atom({
    key: "number1State",
    default: 0,
});

const number2State = atom({
    key: "number2State",
    default: 0,
});

const sumSelector = selector({
    key: "sumSelector",
    get: ({ get }) => {
        const number1 = get(number1State);
        const number2 = get(number2State);
        return number1 + number2;
    },
});
```

---

# 쓰기 가능한 selector

입력 값을 받아서 다른 Recoil State에 변경 사항을 전파

```js {all} {maxHeight: '400px'}
import { atom, selector, useRecoilState, DefaultValue } from "recoil";

const tempFahrenheit = atom({
    key: "tempFahrenheit",
    default: 32,
});

const tempCelcius = selector({
    key: "tempCelcius",
    get: ({ get }) => ((get(tempFahrenheit) - 32) * 5) / 9,
    set: ({ set }, newValue) =>
        set(
            tempFahrenheit,
            newValue instanceof DefaultValue
                ? newValue
                : (newValue * 9) / 5 + 32
        ),
});

function TempCelcius() {
    const [tempF, setTempF] = useRecoilState(tempFahrenheit);
    const [tempC, setTempC] = useRecoilState(tempCelcius);
    const resetTemp = useResetRecoilState(tempCelcius); // default 값으로 리셋합니다.

    const addTenCelcius = () => setTempC(tempC + 10);
    const addTenFahrenheit = () => setTempF(tempF + 10);
    const reset = () => resetTemp();

    return (
        <div>
            Temp (Celcius): {tempC}
            <br />
            Temp (Fahrenheit): {tempF}
            <br />
            <button onClick={addTenCelcius}>Add 10 Celcius</button>
            <br />
            <button onClick={addTenFahrenheit}>Add 10 Fahrenheit</button>
            <br />
            <button onClick={reset}>Reset</button>
        </div>
    );
}
```

---

# 쓰기 가능한 selector

섭씨 컴포넌트에서 값을 변경하면, 섭씨 값이 변경되고, 화씨 값도 변경됨

<img src="https://i.postimg.cc/tJhV3Vrg/recoil-selector.png">

-   setTempF 를 호출하면 tempCelcius Selector의 get에서 tempFahrenheit 가 변경된 것을 탐지
-   tempF, tempC 모두 변경되어 리렌더링

---

# 비동기 selector

selector의 get 함수에서 비동기 작업을 수행할 수 있음

```js
const dataSelector = selector({
    key: "dataSelector",
    get: async ({ get }) => {
        const data = await fetchData(); // 비동기 함수 호출
        return data;
    },
});
```

```js
export default function DataComponent() {
    const data = useRecoilValue(dataSelector); // 비동기 데이터 가져오기

    return (
        <div>
            {/* 데이터를 사용하여 UI를 렌더링 */}
            <h1>{data.title}</h1>
            <p>{data.description}</p>
        </div>
    );
}
```

---

# Suspense를 이용한 비동기 selector

위 DataComponent를 그냥 사용하면 `<Suspense fallback=...>`을 상위 트리에 작성하라는 에러 발생함

```js
import React, { Suspense } from "react";
import DataComponent from "data-component";

const App = () => {
    return (
        <RootRecoil>
            <Suspense fallback={<div>Loading...</div>}>
                <DataComponent />
            </Suspense>
        </RootRecoil>
    );
};

export default App;
```

---

# Loadable을 이용한 비동기 selector

-   Suspense는 Recoil v18 부터 지원 됨
-   이전 버전에서는 `useRecoilStateLoadable`을 사용

```js
import React from "react";
import { useRecoilValueLoadable } from "recoil";
import { dataSelector } from "./selectors";

export default function DataComponent() {
    const dataLoadable = useRecoilValueLoadable(dataSelector);

    switch (dataLoadable.state) {
        case "hasValue":
            return <div>{dataLoadable.contents}</div>;
        case "loading":
            return <Spinner />;
        case "hasError":
            throw dataLoadable.contents;
    }
}
```

-   하지만 비동기 처리는 React Query를 사용하는게 더 높은 상태관리를 제공함

---

# Recoil 내부 구조 Store

Context API를 사용하여 내부적으로 상태를 관리

### Graph ( 의존성 그래프 )

-   상태와 컴포넌트의 의존성을 관리
-   어떤 상태가 어떤 컴포넌트에 영향을 미치는지 추적

<br>

### Tree

-   상태 값들을 트리 구조로 관리
-   AtomNode와 SelectorNode로 구성
    -   Node : 상태를 관리하는 단위. 상태 하나당 Node 하나
-   Store의 상태가 변경되면 Tree를 순회하며 변경된 Atom을 찾아서 BatchUpdate

---

# Recoil Hook

Store의 상태를 읽고, 업데이트 하기 위한 Hook

-   Atom, Selector 별로 Hook이 존재
-   각 상태별로 useEffect의 의존성 배열을 둬서 상태가 변경될 때 마다 useEffect가 호출됨

---

# 마치며

-   Facebook에서 개발된 Recoil은 React의 hook과 사용 방식이 유사하여 **러닝 커브가 매우 낮습니다.**
-   Redux와 비교하여 **간결한 코드**와 **쉬운 상태 관리**를 제공합니다.
-   Recoil은 내부적으로 렌더링 최적화를 수행하지만, 이는 Context API 대비 메모리를 더 사용한다는 단점이 있습니다.
-   Redux와 달리 Recoil은 내장된 DevTools를 통한 상태 변화 추적과 디버깅 기능이 없습니다.

**개발자는 자신의 상황과 상태 관리 방식에 맞는 라이브러리를 선택하여 사용하는 것이 중요합니다.**
