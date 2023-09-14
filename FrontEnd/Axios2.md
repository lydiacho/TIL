## axios란?

- 브라우저, Node.js를 위한 Promise API 기반의 HTTP 비동기 통신 라이브러리
- 프론트엔드 → 백엔드로 서버통신 시 요청과 응답 데이터를 간편히 변형해주는 라이브러리

> 💡 Promise란?
>
> - JS에서 제공하는 **비동기**를 간편하게 처리할 수 있도록 돕는 **객체**
> - Promise 성공 : resolve 함수 호출 (resolve 호출 인자(ex-response) → `.then`에서 활용)
> - Promise 실패 : reject 함수 호출 (인자(ex-error) → `.catch`에서 활용)

JS에는 내장되어있는 **fetch api**가 존재하지만, React 프레임워크에서는 **axios**를 쓴다.

> 💡 Fetch API란?
>
> - ES6로부터 들어온 JavaScript 내장 라이브러리.
>
> 👍🏻 **장점**
>
> - JS 내장 라이브러리이기 때문에 별도의 import 불필요
> - Promise 기반으로 만들어져 데이터를 다루기 쉬움
> - 내장 라이브러리이기 때문에 업데이트에 따른 에러 방지 가능
>
> 👎🏻 **단점**
>
> - 지원하지 않는 브라우저 존재
> - 네트워크 에러 발생 시 response timeout 없이 기다려야 함
> - **JSON으로 변환**해주는 과정 필요 `.json()`
> - 상대적으로 axios에 비해 기능 부족

<br/>

▶️ **axios 의 장단점**

👍🏻 \***\* **장점\*\*

- response timeout 처리 가능
- Promise 기반으로 만들어져 데이터 다루기 편리
- 크로스 브라우징 최적화로 브라우저 호환성 좋음
- JSON 데이터 자동 변환

👎🏻 **단점**

- 별도의 모듈 설치 필요

<br/>

▶️ **axios 의 메소드**

> 💡 data : 객체 리터럴로 전달

- axios.request(config)
- **axios.get(url, ~~**config~~**) : 데이터 조회**
- **axios.delete(url, ~~**config~~**) : 데이터 삭제**
- axios.head(url, ~~config~~)
- axios.options(url, ~~config~~)
- **axios.post(url, data**, ~~config~~**) : 데이터 등록**
  - 필요로하는 자원 정보가 url(query string)에 들어가지 않아서 GET보다 안전
- **axios.put(url, data**, ~~config~~**) : 전체 데이터 수정**
  ```jsx
  axios.put("/update", {
    id: 1,
    name: "개발이 취미인 사람",
  });
  ```
- **axios.patch(url, data,** ~~config~~**) : 툭종 데이터 수정**
  ```jsx
  axios.patch(`/update/${1}`, {
    name: "개발이 취미인 사람",
  });
  ```

> 💡 URL
>
> - `param` : **/path**
> - `query string` : **?id=1**

<br/>

**▶️ axios 의 response 스키마**

Promise의 **resolve** 인자이자, `.then((response)⇒…);` 에서 활용

- `data : { }` - 서버가 제공하는 응답
- `status : 200` - HTTP 상태 코드
- `statusText : ‘OK’` - HTTP 상태 메세지
- `headers : { }` - HTTP 헤더
- `config : { }` - 요청을 위해 Axios가 제공하는 구성
- `request : { }` - 해당 응답으로 생성된 요청.
  - node.js 기준 마지막 ClientRequest 인스턴스
  - 브라우저 기준 XMLHttpReqeust

<br/>

---

<br/>

## axios 사용 모듈화

- **반복적으로 쓰이는 코드**를 추상화하여 효율적인 사용을 도울 수 있다
  - **config 옵션** (baseURL, headers 등 고정적인 config 옵션들)

→ ✅ `axios.create({config})`를 통해 **Axios intance**를 생성하자!

```jsx
// 고정적인 옵션이 baseURL인 경우
// api.ts
import axios, { AxiosInstance } from "axios";

const api: AxiosInstance = axios.create({
  baseURL: import.meta.env.VITE_APP_BASE_URL,
});
```

```jsx
// instance 활용 방식
// 컴포넌트.tsx
...
const fetchData = async () => {
  await api.get('/path')
      .then(res => {})
...
```

<br/>

---

<br/>

## 1️⃣ [ axios ]로 data fetching하기

```jsx
const [requestState, setRequestState] = useState({
  data: [],
  loading: true,
  error: null,
});

const fetchData = async () => {
  try {
    const { data: fetchData } = await api.get("/posts");
    setRequestState((prev) => ({
      ...prev,
      data: fetchData,
    }));
  } catch (err) {
    setRequestState((prev) => ({
      ...prev,
      error: err,
    }));
  } finally {
    setRequestState((prev) => ({
      ...prev,
      loading: false,
    }));
  }
};

useEffect(() => {
  fetchData();
}, []);
```

- async, await을 활용하여 비동기 처리
- try, catch, finally를 이용하여 에러 핸들링 및 로딩 처리

<br/>

▶️ **해당 방식의 한계점**

useState, useEffect, 에러핸들링 로직 등 모든 데이터 패칭에 반복적으로 사용되는 코드가 **각 페이지들마다 중복으로 작성**됨

**→ 🩵중복 코드를 줄이고 재사용하기 위해 custom Hook을 만들어 추상화하자! 🩵**

<br/>

---

<br/>

## 2️⃣ [ axios + 커스텀 훅 ]으로 data fetching하기

> 💡 커스텀훅?
> React Hook을 활용한 특정 상태관리나 라이프사이클 로직들을 재사용하기 위해 추상화한 함수

<br/>

▶️ **일반적인 Hook의 구조**

1. **state (3개)**

   - response
   - error
   - loading

   ```jsx
   const [response, setResponse] = useState<AxiosResponse>();
   const [error, setError] = useState<AxiosError>();
   const [loading, setLoading] = useState(true);
   ```

2. **API와 상호작용하는 함수**

   ```jsx
   const fetchData = async () => {
     await api
       .get("/stickers/custom/hot")
       .then((res) => {
         const response: HotCustomResponse = res.data;
         setResponse(response.data);
       })
       .catch((err) => {
         setError(err);
       })
       .finally(() => {
         setLoading(false);
       });
   };
   ```

   - 로드 시 최초 한번만 호출하기 위한 useEffect

   ```jsx
   useEffect(() => {
     fetchData();
   }, []);
   ```

3. **return 값**

   ```jsx
   return { response, error, loading };
   ```

---

<br/>

## 3️⃣ [ axios + SWR ]로 data fetching하기

TBD…

## 4️⃣ [ axios + React Query ]로 data fetching하기

TBD…
