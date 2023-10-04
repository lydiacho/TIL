### ▶️ “[Intersection Observer API](https://github.com/thebuilder/react-intersection-observer)”

- 브라우저의 Viewport와 특정 Element의 교차점을 관찰하여 사용자의 Viewport에 해당 Element가 보이는지 아닌지를 구별하는 기능 제공
- 한마디로, **element가 사용자의 화면에 보이는지 안보이는지**를 추적할 수 있음

### ▶️ react-intersection-observer 라이브러리

- Web API인 Intersection Observer API를 기반으로 하는 React 라이브러리

### ▶️ 특징

- `useInView` 훅을 사용해서 더욱 쉽게 사용자의 뷰포트를 추적해 객체가 화면에 보이면 특정 코드를 실행시키는 로직을 매우 쉽게 구현할 수 있음
- 컴포넌트 간에 Intersection Observer instance를 공유하기 때문에 여러 요소를 관찰하는 데에도 하나의 인스턴스를 재사용함 → 성능 최적화
- TS로 작성되어있음
- bundle 작음 (~1.15KB for useInView, ~1.6KB for InView)

### ▶️ 필요성

- 해당 API를 이용하지 않을 경우, 사용자의 scroll이 발생할 때마다 element가 Viewport에 담겼는지 체크하는 이벤트 리스너를 실행해야 한다. 이러한 이벤트 발생 횟수를 절감시킴으로써 성능 최적화
- Intersection Observer API는 비동기적으로 작동하기 때문에, 페이지의 주 스레드에 영향을 주지 않음
- Intersection Observer API는 대부분의 주요 브라우저에서 지원됨. (호환성 좋음)

### ▶️ 무한 스크롤?

- 데이터를 한번에 보여주는 성능 낮은 방식과, 사용자 경험이 좋지 못한 페이지네이션 방식 외에, 사용자의 입장에서는 **하나의 페이지를 계속 스크롤 내리는 것처럼 느끼지만, 특정 범위의 데이터만 초기에 불러오고, 사용자의 화면이 현재 목록의 하단에 도달할 때마다 추가로 다음 데이터 범위를 불러와서 보여주는 방식**
  ex) 마켓플레이스에서 상품 목록을 보여줄 때 대부분 사용

### ▶️ 사용 방법

- import
  ```jsx
  import { useInView } from "react-intersection-observer";
  ```
- useInView 생성 및 객체 지정
  ```jsx
  const [ref, inView] = useInView();

    ...

    return (
  	  	<div ref={ref}></div> // 관찰할 객체
    )
  ```
- ref 객체가 Viewport에 포함될 시 특정 함수 실행
  ```jsx
  useEffect(() => {
    if (inView) {
      setPage((prev) => prev + 1);
    }
  }, [inView]);
  ```
  → inView 값이 바뀔 때 (객체가 Viewport에 담긴 것을 감지했을 때) 보여주는 페이지 수 (보여줄 내용 범위)를 1 추가해준다.

### ▶️ useInView Hook

- 특정 컴포넌트의 `inView` 상태를 쉽게 모니터할 수 있도록 돕는 훅

```tsx
// 기본 형태
const { ref, inView, entry } = useInView(options);
```

- ref : 모니터하고 싶은 DOM element에 지정
- inView : Viewport에 포함됐는지를 관리하는 상태
- entry : IntersectionObserverEntry (관련 세부 정보)
- 여러 [options](https://github.com/thebuilder/react-intersection-observer#options) 세팅 가능
  - 대표 option : `threshold`
    → 0.0~1.0까지의 숫자로, 지정한 객체가 **어느정도의 비율이 보일 때** 함수를 실행할지 지정
