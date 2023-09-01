### 📌 한줄 정리 : Vite는 기존에 사용하던 Webpack 번들러의 속도를 개선한 빌드 도구이다.

# Vite 알아보기

![스크린샷 2023-09-02 오전 2.04.25.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1d40a623-da7d-44e1-9004-b5b5a8861918/46d14608-56de-4fec-a7b8-0acdf2e77957/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2023-09-02_%EC%98%A4%EC%A0%84_2.04.25.png)

Vite(비트)는 프론트엔드 개발을 위한 빌드 도구이다.

Vite가 등장한 배경을 알아보기 위해 우선 CRA (Create React App)에 대해 알아보자.

## CRA

Create React App

React를 만든 페이스북이 편리한 React 개발을 위해 제공하는 CLI 도구이다.

CRA로 React 프로젝트를 만들 때, **Webpack** 이라는 번들러를 사용한다. (웹팩에 대한 설명은 하단에)

그런데 이 웹팩은 인터프리터 언어인 JavaScript 코드로 구성되어있어 코드가 많아질 수록 속도가 저하된다는 한계점을 가진다

따라서 이러한 한계점을 개선하고자 Go 언어와 같은 Low-level 언어를 활용하여 빌드 속도를 개선한 JS 툴을 만들었고, 대표적인 사례가 **ESbuild**이다.

그리고 이 ESbuild를 기반으로 만들어진 빌드 도구가 바로 **Vite**이다.

## Vite

공식 문서에서는 Vite(비트)를 **빠르고 간결한 모던 웹 프로젝트 개발 경험에 초점을 맞춰 만들어진 빌드 도구**라고 소개한다.

Vite가 처음 등장할 때 `리액트가 10배 더 빨라집니다` 라는 문구를 내세웠다고 한다.

비트는 ESM(ECMAScript Modules), HMR(Hot Module Replacement), ESBuild 등을 다양한 기능들을 활용하여 서버가 구동되는 시간, 번들링 속도, 코드 갱신 속도 등을 개선하였다.

현재 출시된지 3년 이상이 되어 웹팩이 제공하는 다양한 기능들과의 호환성도 많이 안정된 상태이지만,

아직까지도 리액트 시장에서 웹팩의 영향력이 더 우세하다는 것은 틀림 없다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1d40a623-da7d-44e1-9004-b5b5a8861918/110edf4c-cca0-4ce4-b4ee-f22496ce7df0/Untitled.png)

Vite의 특징은 다음과 같다.

- Node.js를 설치해야만 사용할 수 있다
- 프론트엔드와 관련된 다양한 프레임워크, 라이브러리에 대한 템플릿을 제공한다
- CRA보다 패키지 관리도 더 편리하다
- 서비스 규모가 커서 추가적인 번들링 도구를 필요로 할 땐 rollup 이라는 번들링 도구를 사용한다.

### Vite 시작하기

- `yarn create vite` / `yarn create vite@latest {프로젝트명}`
- 순차적으로 프로젝트명, 프레임워크, variant를 선택한다
  - vite가 지원하는 템플릿 : vanilla, vue, react, preact, lit, svelte

---

## ▶️ Webpack?

웹팩은 오픈 소스 JavaScript **모듈 번들러**이다.

웹사이트를 개발할 때 HTML, CSS, JS, 이미지 파일 등 많은 리소스 파일을 불러오느라 서버 접속 및 로딩 속도가 지체될 떄가 있다.

이로 인한 사용자 이탈을 막고자,

- 클라이언트에서 여러 파일들을 압축 및 병합(Bundling)하여 한 번에 서버로 요청하는 방식
- 초기 로딩 시 모두 불러오는 것이 아닌, 각 리소스가 필요할 때마다 요청하는 방식(Lazy Loading)을 통해 로딩 시간을 개선하자는 철학

이러한 솔루션을 가지고 등장한 것이 **웹팩**이다.

> **Module** **Budling?** 모듈화 하는 과정에서 각 파일의 의존성을 추적하여 그룹핑을 해주는 것이 Bundling이고 해당 역할을 하는 도구가 번들러, 대표적인 사례가 웹팩이다.
