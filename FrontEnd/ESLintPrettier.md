# ESLint & Prettier

ESLint와 Prettier는 목적은 같으면서도 다른 역할을 한다.

둘다 **일관성 있는 코드**를 위해 사용하는 도구이지만,
ESLint는 **코드 구현 방식**을,
Prettier는 **코드 작성 스타일**을
통일시켜주는 역할을 한다.

> Index
> 1. VSCode에서 ESLint와 Prettier 사용하기
> 2. ESLint
> 3. Prettier

## VSCode에서 ESLint와 Prettier 사용하기

- VS 코드에서 Extenstion으로 **ESLint**와 **Prettier - Code formatter**을 설치한다.
- Setting (단축키 : `cmd`+`,`) 에서 Default formatter로 Prettier를 설정해준다.
<img width="694" alt="%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-09-02%20%EC%98%A4%ED%9B%84%206 31 22" src="https://github.com/lydiacho/TIL/assets/81505421/0d94c8fc-e6c3-4a8d-a901-dbda4da3e52a">

- 저장할 때마다 포맷이 적용되도록 설정하는 체크박스
<img width="739" alt="%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-09-02%20%EC%98%A4%ED%9B%84%206 32 04" src="https://github.com/lydiacho/TIL/assets/81505421/9135f965-648f-4b7c-9746-89c1f0e0f91e">


## ESLint

[공식 문서](https://eslint.org/docs/latest/)

사용자가 규칙을 구성한 후, 해당 규칙에 어긋나는 JavaScript 코드를 찾아주는 **정적 코드 분석 도구**이다.

➡️ **세팅**

앞선 글에서 빌드 도구 Vite에 대해 알아보았다. 따라서 Vite로 프로젝트를 생성하는 경우를 고려하여 설명하겠다.
Vite를 통해 React (variant : TypeScript) 프로젝트를 생성하면 **.eslintrc 파일**이 자동으로 생성된다.

```jsx
// 최초 세팅되어있는 .eslintrc.cjs
module.exports = {
  root: true,
  env: { browser: true, es2020: true },
  extends: [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react-hooks/recommended",
  ],
  ignorePatterns: ["dist", ".eslintrc.cjs"],
  parser: "@typescript-eslint/parser",
  plugins: ["react-refresh"],
  rules: {
    "react-refresh/only-export-components": [
      "warn",
      { allowConstantExport: true },
    ],
  },
};
```

- **env** : 사전에 정의된 전역 변수(공식 문석에서 참고 가능) 사용 정의
  > browser : browser global variables

  > es2020 : adds all ECMAScript 2020 globals and automatically sets the ecmaVersion parser option to 11.
- **extends** : eslint 규칙 설정이 담긴 외부 파일을 불러오는 부분
  - `recommended` 는 기본 세팅 (말그대로 추천해주는 세팅) 그대로 설정한다는 의미이다.
  - 이곳에 추가하면 각 모듈 내부의 .eslintrc가 알아서 적용된다
- **parser** : 코드 파일을 검사하는 프로그램
  - TypeScript로 코드를 작성할 땐 위와 같이 `@typescript-eslint/parser`로 설정해주어야 한다
- **plugins** : ESLint가 지원하는 서드파티 플러그인
- **rules** : 추가적인 룰을 세팅하고 싶을 때 추가
  - https://eslint.org/play/ 에서 편리하게 세팅 가능

> ESLint 옵션이 매우 구체적으로 설명되어있는 자료이다 👉🏻 [참고](https://www.daleseo.com/eslint-config/)

<br/>

💡 개인적으로 extends와 plugins의 역할이 무슨 차이인지 이해가 가지 않아 더 공부해 보았고, 간단히 정리하면 다음과 같다.

- extends : 플러그인 내부 rule을 불러와서 통째로 적용
- plugins : 플러그인 내부 rule을 적용시킬 수 있도록 불러오기만 함
- rules : 불러온 플러그인 내부 rule 중 적용시킬 특정 rule 정의

즉, **extends = plugins + rules** 인셈!

<br/><br/>

➡️ **package.json**

package.json의 scripts에는 vite로 인해 lint 명령어가 세팅되어있을 것이다.

필요에 따라 `lint:fix`도 추가해줄 수 있다

```jsx
// 내 프로젝트 예제

"lint": "eslint src --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
"lint:fix": "eslint src --ext .ts --parser-options=project:'tsconfig.json' --fix",
```

- lint : lint 규칙을 지켰는지 확인해주는 명령어
- link:fix : lint 규칙을 지켰는지 확인하고 지키지 않았다면 고쳐주는 명령어

<br/>

> 📢 주의! 종종 lint 검사를 할 때, import React를 안해서 전체 코드에 빨간 줄이 그어질 때가 있다. 이 때엔, 모든 파일에 import React를 해주는 번거로움을 사지 말고 eslintrc 파일의 rules에 **'react/react-in-jsx-scope': 'off'** 구문을 추가해주자

<br/><br/>

## Prettier

[공식문서](https://prettier.io/docs/en/options)

JavaScript에서 가장 많이 쓰이는, 말그대로 더 예쁜 코드를 만들어주는 **코드 포맷터**이다.
협업 시, 각 팀원들 간의 코드 스타일이 다를 경우 버전 관리에서 같은 내용의 코드도 다르게 여겨지는 등 코드가 뒤섞여버리기 때문에 Prettier 사용은 필수적이라고 할 수 있다.

➡️ **세팅**

- `yarn add -D prettier eslint-config-prettier eslint-plugin-prettier`
  - eslint-config-prettier, eslint-plugin-prettier : eslint와 prettier의 호환성을 높여주는 플러그인

Prettier 옵션 설정은 CLI 명령어로도 가능하고, package.json에 옵션을 작성하는 방식도 있지만,
요즘 가장 많이 쓰이는 편리한 방식은 루트 디렉토리에 `.prettierrc` 파일을 생성해 이곳에서 세팅하는 것이다.
왜냐하면 프로젝트 디렉토리를 처음 보고 곧바로 prettier 사용 여부를 알 수 있으며, 쉽게 내부 구조를 읽어볼 수 있기 때문이다.

> `.prettierignore` 파일 : 프리티어 포맷팅을 적용하지 않을 파일의 경로를 작성하면 된다

```jsx
// 내 프로젝트 .prettierrc.cjs 예제

module.exports = {
  bracketSpacing: true,
  singleQuote: true,
  tabWidth: 2,
  trailingComma: "all",
  printWidth: 100,
  endOfLine: "auto",
  useTabs: false,
  semi: true,
  jsxSingleQuote: true,
  arrowParens: "always",
};
```

- **bracketSpacing** : 중괄호 안쪽에 공백 추가
- **singleQuote** : true - 문자열쓸 때 `“` 말고 `‘`
- **tabWidth** : 2 - 탭 너비 공백 2칸
- **trailingComma** : all - 모든 경우 배열이나 객체 요소가 여러 줄에 걸쳐 작성될 때 맨마지막에도 , 붙음
- **printWidth**: 한줄 최대 글자 수 (디폴트 80)
- **endOfLine**: 개행 세팅
- **useTabs**: 탭 문자로 들여쓰기
- **semi** : 세미콜론을 붙여야 함
- **arrowParens** : 화살표 함수 시 매개변수 개수와 무관하게 소괄호로 감싸야 함

> `.prettierrc` 작성을 돕는 사이트 : [https://prettier.io](https://prettier.io/)

<br/><br/>

➡️ **package.json**

script 에 prettier를 체크하는 명령어도 추가해줘야 하는데,
우리 프로젝트는 husky와 lint-staged를 사용했기 때문에 (+TS 사용)
다음과 같이 추가하였다.

```jsx
"lint-staged": {
  "*.{ts,tsx}": [
    "prettier --write",
    "eslint --fix"
  ]
},
```
