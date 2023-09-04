## Directory Structure

- feature 단위가 아닌 function 단위
  - 에시
    - feature 기준 디렉토리 : base, search, users …
    - function 기준 디렉토리 : components, utils, helpers, hooks, constants
  - feature 단위의 디렉토리 구조의 단점 :
    - 실상은 각 feature에 따라 분명하게 분리하는 것이 매우 어렵다.
    - 경계가 매우 모호하기 때문에 각 개발자마다의 주관에 따라 판단이 달라질 수 있어 컴포넌트를 생성할 때마다 해당 컴포넌트가 어느 feature에 속해야 할지 논의해야 한다.
    - 가장 치명적인 단정믄, 서비스는 꾸준히 변화하곤 하는데, 이에 따라 **리팩토링**을 할 경우 기능이 조금만 바뀌어도 디렉토리 구조상의 대공사가 요구된다는 점이다.

➡️ **Components**

- 관련 파일이 많은 복잡한 컴포넌트의 경우, `src/components/컴포넌트명/` 디렉토리의 하위에 관련 파일을 모아놓는다.
  - 특정 컴포넌트에 귀속된 파일들은, 해당 컴포넌트를 개발할 때만 접근하기 좋도록.
  - 하위 컴포넌트, 유틸 함수, 커스텀훅, 상수 혹은 공용 데이터 등

➡️ **Hooks**

- 훅이 특정 컴포넌트에 종속되는 경우엔 컴포넌트 디렉토리 하위에 속한다.
- 하지만 대부분의 훅은 여러 컴포넌트에 공용으로 쓰이고, 이럴 경우 `src/hooks` 디렉토리에 별도로 모아둔다.

➡️ **util**

- 추상적인 태스크를 처리하는 일반적인 함수
- `src/util.js` 에 유틸 함수를 모아두기
- 해당 유틸 함수는 특정 프로젝트에 귀속되는 것이 아닌, 모든 프로젝트에 자주 쓰이는 경우가 많아서 `src/util.js` 파일을 매 프로젝트마다 옮겨붙여 기본 세팅으로 추가하는 경우도 많다.

➡️ **constants**

- `constants.js` 파일을 생성
- 서비스 전반에 필요한 상수를 모아놓는다.
- ex) 스타일과 관련된 데이터 (색, 폰트 사이즈, 퍼블릭 키 등)

➡️ **pages**

- 페이지 디렉토리가 프로젝트 빌드 도구에 따라 필요할 수도 있고, 필요 없을 수도 있다
- 각 route 마다 여러 컴포넌트들을 합친 **구조**를 정의하는 상위 컴포넌트가 존재할 경우, `src/pages/` 디렉토리를 사용

<br/>

## 절대경로 설정 (alias)

절대경로에 별칭을 만들어 붙일 수 있다.

```jsx
// 기존
import { sortCategories } from "../../helpers/category.js";

// alias 사용
import { sortCategories } from "@helpers/category.js";
```

`/src/helpers` 디렉토리에 `@helpers` 라는 alias를 설정하면,

이후 번들러가 별칭을 해당하는 **상대경로로** 변환시켜준다.

- 장점 :
  - 코드가 전반적으로 간결해진다.
  - depth가 깊어질 수록 작성하기 다소 번거로운 상대경로 대신 절대경로를 사용할 수 있게 해준다.
    - ../ ../ ../…. 얼마나 여러번 상위 디렉토리를 타고 올라가야 하는지 고려할 필요가 없어진다
  - 파일의 경로를 이동하더라도, 모든 import문을 수정할 필요가 없어진다.
  - 어떤 컴포넌트/파일을 참조하는 것인지 명시적으로 확인 가능하다.

<br/>

**➡️ JavaScript) vite.config.js 파일에서 세팅**

- defineConfig
  - resolve
    - alias

에 있는 배열에

- find : 절대 경로 별칭 (@로 시작)
- replacement : 대체할 절대 경로

로 이루어진 객체를 추가하면 된다.

```jsx
// vite.config.js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react-swc";

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: [
      { find: "@", replacement: "/src" },
      { find: "@pages", replacement: "/src/pages" },
    ],
  },
});
```

<br/>

**➡️ TypeScript) tsconfig.json & vite.config.ts 파일에서 세팅**

1. **tsconfig.json** 파일에서 `compilerOptions` 내부에

- `baseUrl` : 기본 경로
- `paths` : { 별칭 : [ 기본 경로 기준 절대 경로 ] }

를 추가한다.

```jsx
"compilerOptions": {
	// ...
    "baseUrl": ".",
    "paths": {
      "@helpers/*": [
        "src/components/*"
      ],
    },
		"include": ["src", "**/*.ts", "**/*.tsx"],
	  "references": [{ "path": "./tsconfig.node.json" }]
  },
```

2. **tsconfig에서 추가한 path를 vite에 등록**

2-1. JS 경우와 같이 vite.config.js - resolve - alias 를 세팅하여 설정할 수 있다.

2-2. `vite-tsconfig-paths` 플로그인을 설치한다.

```powershell
yarn add -D vite-tsconfig-paths
```

**vite.config.ts** 파일에서

- `tsconfigPaths` import
- **plugins**에 `tsconfigPaths()` 추가

```jsx
// vite.config.ts

import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tsconfigPaths from "vite-tsconfig-paths";
// https://vitejs.dev/config/
export default defineConfig({
  base: "./",
  plugins: [react(), tsconfigPaths()],
  // ...
});
```
