## For what? ⇒ 주소지 검색을 위한 API
- 버튼 클릭 시 모달 켜짐
- 주소 선택 시 모달 자동 닫힘
- 주소 선택 시 우편번호, 기본주소가 input에 작성됨
- input은 언제나 disabled (사용자가 임의 편집 불가)

> **💡 sol) `react-daum-postcode` 라이브러리**

### ✔️ 사용방법

1. **설치** : `yarn add react-daum-postcode`
2. `import Postcode from "react-daum-postcode";`

   → Postcode 컴포넌트 : 주소 검색 시 나타나는 모달

3. **UI 구성** : `input`, `button`, `Postcode` 배치하기

   - **input**은 비활성화 (사용작가 임의로 입력하지 못하도록) `disabled`
   - 우편 번호와 주소 들어가는 칸 분리
     - `<input id="post_code" type="text" disabled/>`

   ```html
   <input id="input" type="text" disabled />
   <input id="post_code" type="text" disabled />
   <button type="button">검색</button>
   <div className="card">
     <Postcode />
   </div>
   ```

4. **useState을 통해 모달 open 여부 관리하기**
   - `const [isPostOpen, setIsPostOpen] = useState(false);`
   - `isPostOpen`에 따른 조건부렌더링 추가
     ```html
     {isPostOpen && (
     <div className="card">
       <Postcode onComplete="{handleAddress}" />
     </div>
     )}
     ```
5. **버튼 `onClick`에 모달을 여는 핸들러 `handleModal` 달아놓기**

   ```jsx
   const handleModal = () => {
     setIsPostOpen(true);
   };
   ```

6. **Postcode의 `onComplete`에 주소 검색 완료 시 실행할 핸들러 `handleAddress` 달아놓기**

   - 핸들러의 인수로 data를 받고 console.log를 찍어보자.
   - 최종 주소 선택 시 아래처럼 data가 찍히고 모달창은 **자동으로** 닫힌다

   <img width="543" alt="스크린샷 2023-07-01 오전 2 52 13" src="https://github.com/lydiacho/TIL/assets/81505421/85dfdb5f-2564-4ce3-91cf-c8e1540dcbb9">


   여기서 우리가 필요한 값은 주소인 `address`,와 우편번호 `zonecode` !

   → `data.address`와 `data.zonecode`로 value 뽑아내자.

   - 주의! 모달이 자동으로 닫힌다고 `isPostOpen` false 처리해주는 것을 잊으면 안된다!

   ```jsx
   const handleAddress = (data) => {
     document.getElementById("input").value = data.address; // 주소
     document.getElementById("post_code").value = data.zonecode; // 우편번호
     setIsPostOpen(false);
   };
   ```

7. **마지막으로, 뽑아낸 value를 input의 value로 넣어줘야한다.**

- 주소 : `document.getElementById('input').value = data.address;`
- 우편번호 : `document.getElementById('post_code').value = data.zonecode;`

**[ Full code ]**

```jsx
import "./App.css";

import { useState } from "react";
import Postcode from "react-daum-postcode";

function App() {
  const [isPostOpen, setIsPostOpen] = useState(false);

  const handleModal = () => {
    setIsPostOpen(true);
  };

  const handleAddress = (data) => {
    document.getElementById("input").value = data.address;
    document.getElementById("post_code").value = data.zonecode;
    setIsPostOpen(false);
  };

  return (
    <>
      <input id="post_code" type="text" disabled />
      <input id="input" type="text" disabled />
      <button type="button" onClick={handleModal}>
        검색
      </button>
      {isPostOpen && (
        <div className="card">
          <Postcode onComplete={handleAddress} />
        </div>
      )}
    </>
  );
}

export default App;
```

## 구현 결과물



https://github.com/lydiacho/TIL/assets/81505421/1042cf68-c29b-4ac5-8a4a-2b37154b6084


