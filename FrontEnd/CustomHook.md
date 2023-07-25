# Custom Hook

### 커스텀 훅이란?

- 상태 로직을 재사용할 수 있도록 하는 기능
- 여러 컴포넌트에서 **공통적으로 사용되는 상태 로직을 추출**하여 하나의 함수로 만듦 = **캡슐화**
- 함수 이름은 `use` 로 시작
- React의 기본 **훅**들 (useState, useEffect 등)을 사용해서 구현

### 커스텀 훅을 사용하는 이유?

- 중복된 코드 방지
- 코드의 **재사용성 및 유지보수성** 향상
- 커스텀 훅으로 자주 구현되는 기능 : **API 호출**, 폼 데이터 관리, 타이머/애니메이션 등

### 커스텀 훅과 유사한 유틸 함수

- 유틸 함수는 React에서 자주 사용되는 기능을 모듈화한 함수를 말한다
  - 결국, 프로젝트에서 자주 사용하는 함수를 별도의 파일로 관리하는 개념
- 유틸 함수 또한 코드의 재사용성 및 유지보수성 향상을 위해 구현된다

### 예제

타이머를 활용하여 매 초마다 데이터를 업데이트 하는 커스텀훅

```jsx
import { useState, useEffect } from "react";

function useTimer(initialTime) {
  const [time, setTime] = useState(initialTime);

  useEffect(() => {
    const timer = setInterval(() => {
      setTime((prevTime) => prevTime + 1);
    }, 1000);

    return () => clearInterval(timer);
  }, [initialTime]);

  return time;
}
```
