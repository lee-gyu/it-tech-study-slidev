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
   <v-click>
   <img src="https://i.postimg.cc/NM7SZYfS/recoil.png" style="">
   </v-click>

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

# Context API의 문제점

-   상태의 복잡도를 간소화시킬 수는 있음
-   React 공식 문서에서 Context를 자주 사용하는 것을 권고하지 않음<br/><br/>

<v-click>
    <p>1.특정 Context에 의존하기 때문에 컴포넌트간 결합도 증가 => 재사용 어려움</p>
</v-click>
<v-click>
    <p>2. 상태 변경 시 Context를 구독하고 있는 모든 컴포넌트가 리렌더링 됨</p>
    <img src="https://i.postimg.cc/W30yRVSg/context.jpg" style="width: 40%;">
</v-click>

---

# Context API 언제 써야하나?

### React 공식 문서

-   전역적 ( global ) 데이터를 공유할 때
    > context는 React 컴포넌트 트리 안에서 전역적(global)이라고 볼 수 있는 데이터를 공유할 수 있도록 고안된 방법입니다.<br/>
    > 그러한 데이터로는 현재 로그인한 유저, 테마, 선호하는 언어 등이 있습니다.

<br/>

### 결론

-   Context는 전역적으로 데이터를 공유하는 API
-   전역 상태를 관리하기 위한 API가 아님
    <v-click>
    <p style="fontWeight:bold;">낮은 빈도로 업데이트가 일어나는 데이터를 공유할 때 사용하는 것이 좋음</p>
    </v-click>

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
    <v-click>
    <p style="fontWeight: bold">Redux Boilerplate</p>
    <p>Action</p>
    <p>Reducer</p>
    <p>Dispatch</p>
    <p>Store</p>
    </v-click>

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

# Redux의 단점

-   상태 관리를 위한 비용이 많이 듦
-   반응형 업데이트, 비동기 처리 등을 위해 라이브러리를 추가로 사용해야 함
    -   redux-thunk
    -   redux-saga
    -   redux-toolkit
        <br/><br/>

### 결론

러닝커브가 높고, 비용이 많이 들어서 Redux를 사용하기 위해 많은 시간을 투자해야 함

---

# Recoil은 어떻게 다른가요?

-   React를 구현한 Facebook에서 만든 상태 관리 라이브러리
-   **배우기 쉽다**
-   hook과 동일한 사용방식
