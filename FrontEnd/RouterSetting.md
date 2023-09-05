# 라우터 초기세팅

## 라우팅?

- 사용자가 요청한 링크 주소(URL)에 해당하는 페이지를 찾아서 보여주는 것
- URL의 경로와 query 부분을 분석하여 해당하는 컴포넌트를 렌더링
- 뒤로 가기 / 앞으로 가기 버튼과 같은 브라우저 기능과의 호환성을 위해 필요함

▶️ **라우팅 방식**

- `MPA` 방식
  - Multi Page Application
  - 여러 페이지를 분리해두고, 페이지간 이동으로 라우팅
  - 초기 로딩 시 서버에서 컨텐츠를 한꺼번에 불러옴
- `SPA` 방식
  - Single Page Application
  - 로딩할 때마다 그때그때 필요한 데이터만 서버에서 가져옴
  - React의 라우팅 방식. `react-router` 라이브러리 사용
    - `react-router` [라이브러리](https://reactrouter.com/en/main) : URL의 업데이트에 따라 해당하는 컴포넌트를 선택하여 렌더링

▶️ **SPA 방식**

말그대로 하나의 페이지로 구성된 애플리케이션이다.

따라서 기존의 방식이었다면 페이지를 이동해야할 때, SPA 방식은 고정되어있는 페이지에서 **필요한 컴포넌트만 갈아끼워주며 동적으로 페이지를 업데이트**한다.

매번 새로운 페이지를 이동하면서, 페이지에 필요한 HTML, CSS, JS, 에셋 등을 매번 새로이 다운받는 방식이 아니기 때문에 당연하게도 **로딩 속도가 개선**되며 **사용자 경험이 향상**된다.

특히! SPA는 저사양 기기에도 빠르게 작동하기 때문에 **모바일 최적화 애플리케이션**에 매우 적합하다고 한다.

## react-router-dom을 통해 리액트 라우터 사용

▶️ **라이브러리 설치**

- `yarn add react-router-dom`
  - TypeScript : `@types/react-router-dom`

▶️ **프로젝트에 Router 적용**

- 렌더링되는 컴포넌트의 **최상단**을 `BrowserRouter` 컴포넌트로 감싸기
  - 최상단 컴포넌트 정의는 루트파일에서 이루어진다
  - 루트파일 : index.tsx or main.tsx or App.tsx or Router.tsx … so on
- **BrowserRouter**
  - 웹 애플리케이션에서 HTML5의 **History API**를 통해 페이지 불러오지 않고도 주소를 변경하고, **현재 주소의 경로 정보**를 프로젝트에서 사용할 수 있도록 돕는 컴포넌트
  - `react-router-dom`에서 import 해서 쓰기

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import { BrowserRouter } from "react-router-dom";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

▶️ **Route 컴포넌트 설정**

Routes, Route 컴포넌트 사용

- `react-router-dom`에서 import 해서 쓰기

- **<Routes>** 컴포넌트 : 여러 Route를 감싸서 그 중 필요로 하는 Route를 찾아 렌더링해주는 역할
- **<Route>** 컴포넌트 :
  `<Route path='/pageA' element={<PageA />} />`
  - `path` : 경로
  - `element` : 보여주고 싶은 컴포넌트

```jsx
import { Route, Routes } from "react-router-dom";
import "./App.css";
import About from "./pages/About";
import Home from "./pages/Home";

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
    </Routes>
  );
}

export default App;
```

## **나의 프로젝트에서 라우팅 설정한 방식**

▶️ **main.tsx**

- `App.tsx` 렌더링

▶️ **App.tsx**

- `Router.tsx` 렌더링

▶️ **Router.tsx**

```jsx
const Router = () => {
  return (
    <BrowserRouter>
      <ScrollToTop />
      <Routes>
        <Route path="/list" element={<ListPage />} />
        //...
        <Route path="/error" element={<ErrorPage />} />
      </Routes>
    </BrowserRouter>
  );
};
```

- 최상단에 묶어주는 `BrowserRouter`을 이곳에서 사용했다!

✅ 결국 나의 프로젝트에서 렌더링되는 순서는 다음과 같다

`<main/>` → `<App/>` → `<Router/>` → `<BrowserRouter>` - `<Routes>` - 각 `<Route/>`
