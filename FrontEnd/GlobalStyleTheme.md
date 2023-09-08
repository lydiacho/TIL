## GlobalStyle

프로젝트에서 전역으로 사용할 스타일드 컴포넌트를 하나의 파일에서 정리해준다.

- 공통으로 적용시키고 싶은 스타일
- 디폴트로 들어가있는 스타일을 삭제 (css 초기화)

Styled-Components를 쓰지 않는 일반 css에서는 `reset.css` 파일로 이 역할을 해주었다.

**▶️ 사용법**

- **styled-components** 라이브러리 설치
- **GlobalStyle.ts** 파일 생성
- styled-components에서 `createGlobalStyle` import

```jsx
import { createGlobalStyle } from "styled-components";

const GlobalStyle = createGlobalStyle`
	// 내용작성
`;
```

- App.tsx에서 생성한 GlobalStyle 파일을 import 해준다

```jsx
import GlobalStyle from "./styles/GlobalStyle";
```

- 렌더링하는 컴포넌트 위에 GlobalStyle을 추가해준다

```jsx
<>
  <GlobalStyle />
  <Router />
</>
```

그럼 프로젝트의 전역에 해당 스타일이 적용된다!

**▶️ 전역 스타일링 예시 종류**

TBD

---

## Theme

프로젝트 전반에 자주 쓰이는 스타일들에 있어 휴먼 에러를 줄이고,

고정적인 역할의 스타일에 대해 어떤 역할을 하는지 코드에서 명시적으로 보여줄 수 있다.

주로 자주 사용하는 색상과 폰트에 사용된다.

(디자인 측에서 ‘디자인 시스템’을 지정해주면 초기 세팅 때 이를 참고하여 theme.ts 파일을 작성해주면 된다)

**▶️ 사용법**

- **styled-components** 라이브러리 설치
- **theme.ts** 파일 생성
- styled-components에서 `DefaultTheme` import
- 전역적으로 사용할 스타일 변수를 생성한다.
  - 주로 객체 형태로 생성하여, `큰 카테고리.세부명` 으로 접근 가능하도록 한다.
  ```jsx
  // 예시
  const colors = {
    white: "#FFFFFF",
    bg: "#F7F7FA",
    gray1: "#D8D9DD",
    gray2: "#B2B4BA",
    pink1: "#FFD7E1",
    pink2: "#FFAFC2",
    red: "#FF4444",
    brown: "#392020",
  };
  ```
  - 보통 `colors`, `fonts` 를 사용한다
- `App.tsx`에서 ThemeProvider와 생성한 theme 파일을 import 해준다

```jsx
import { ThemeProvider } from "styled-components";
import theme from "./styles/theme";
```

- 렌더링하는 컴포넌트를 ThemeProvider로 감싸주고, 속성으로 생성한 theme을 전달한다

```jsx
<ThemeProvider theme={theme}>
  <GlobalStyle />
  <Router />
</ThemeProvider>
```

**▶️ ThemeProvider**

> ThemeProvider는 **ContextAPI**를 이용해 리액트 **컴포넌트에게 Theme 속성**을 전달할 수 있으며, 컴포넌트의 depth가 깊어지더라도 루트 위치에 ThemeProvider가 있다면 **모든 렌더 트리의 자식**에는 theme 속성을 가지게 된다.
