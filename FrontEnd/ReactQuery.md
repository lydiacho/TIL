## React Query 란?

React에서 `데이터 fetching`과 `캐싱 프로세스`를 간소화해주는 **라이브러리**

- 외부(API 등)로부터 데이터를 fetching 및 업데이트 과정 간소화
- API 요청의 로딩 및 오류 상태 관리
- 캐싱 자동 관리

<br/>

## Client State vs Server State

|  | Client State | Server State |
| --- | --- | --- |
| 위치 | 클라이언트에 저장된 데이터 | 서버나 외부 데이터 소스에 저장된 데이터 |
| 접근성 | 클라이언트만 접근 가능 | 접근 권한이 있는 모든 클라이언트 접근 가능 |
| 데이터 관리 | 클라이언트에서 관리 <br/> (Redux, Recoil 등 상태관리 라이브러리 사용) | 서버에서 관리 <br/>(데이터베이스 사용) |
| 지속성 | 세션 간에 필연적으로 지속되진 않음  | 일반적으로 세션 간에 지속성 유지 |
| 네트워크 요청 | 데이터를 가져오거나 업데이트하려면 네트워크 요청이 필요할 수 있음 | 데이터 접근 또는 업데이트를 위해 네트워크 요청이 필요할 수 있음 |
| 보안 | 클라이언트가 액세스할 수 있고 보안 수준이 낮음 | 인증 및 암호화로 보호할 수 있으므로 더 안전 |
| 성능 | server state에 비해 속도 빠름 | client state에 비해 속도 느림 |
| 확장성 | 클라이언트 기기 용량이 제한적이어서 확장성이 다소 떨어짐 | 전용 서버나 데이터 소스로 관리되기 때문에 용량이 커서 확장성이 비교적 높음 |
| 예시 | 컴포넌트 state, Redux state, 브라우저 쿠키 | DB 레코드, API 응답, 서버 세션 데이터 |

기존의 Client State 관리는

- Redux
- React Context API
- Recoil

등의 라이브러리를 통해 관리한다.

<br/>


Client에서 API와 통신을 하기 위해서는
추가적으로 **useEffect**, **useState**를 함께 쓰면서 데이터를 fetching 해왔다.

하지만 React Query를 사용하면 이러한 훅들의 필요성이 사라진다.

<br/>


## React Query 주요 개념

`Query`
- API 엔드포인트, DB 등의 원격 데이터 소스로부터 데이터 요청
- **useQuery** 훅 사용

`Mutation`
- 서버에 데이터를 추가하거나 업데이트
- **useMutation** 훅 사용

`Query Caching`
- Query 결과를 메모리에 저장
`Query Invalidation`
- 쿼리를 오래된 상태로 여겨 무효화

<br/>

## 1️⃣ useQuery 훅

> **데이터 Fetching 용**

API 엔드포인트나 DB에서 데이터를 **비동기적**으로 가져오도록 서버에 요청하는 것

<br/>

### **사용법**

```jsx
const query = useQuery( { queryKey: [ ‘key’ ],   queryFn: callback })
```

`queryKey` 
- 쿼리의 **고유 키**
- React Query 최신 버전부터는 **배열 표기법**을 사용해서 키 지정

`queryFn` 
- 훅 호출 시 실행되는 **Promise 반환하는 함수**
- 해당 callback함수에서 데이터 fetching

```jsx
// 예시
const getProducts = () => fetch( 'https://jsonplaceholder.typicode.com/users')
                          .then( res  => res.json() )

const query = useQuery( { queryKey: [‘users’],   queryFn: getTodos })
```

`반환값` 쿼리의 상태 정보를 담고 있는 **객체**

```jsx

const { isLoading, isError, data, error, refetch, remove } = useQuery( { queryKey: [‘todos’], queryFn: getTodos });
```

대표적인 **프로퍼티**

- `isLoading` 쿼리가 현재 로딩 중인지 여부 (boolean)
- `isError` 쿼리 결과가 오류인지 여부 (boolean)
- `data` 쿼리를 통해 성공적으로 fetching된 데이터
- `error` 쿼리 실행 중 발생한 모든 에러
- `refetch` 쿼리 데이터를 수동으로 refetch 하는 트리거 **메소드**
- `remove` 캐시에서 특정 쿼리 제거하는 **메소드**

<br/>

### 데이터 refetching

`useQuery`는 기본적으로

- **컴포넌트 최초 mount 시**에 데이터를 fetching해오고,
- 이후의 데이터 업데이트에 대해서는 **자동 실행되지 않는다. (데이터 refetching 안해줌)**

<br/>

**[ useQuery 옵션 ]**

| 옵션                 | 역할                                                         | 기본값 |
| -------------------- | ------------------------------------------------------------ | ------ |
| refetchOnWindowFocus | 데이터가 오래된(stale) 경우 브라우저 창이 포커스 되면 리페치 | true   |
| refetchOnMount       | 데이터가 오래된 경우 마운트 시 리페치                        | true   |
| refetchOnReconnect   | 데이터가 오래된 경우 재연결 시 리페치                        | true   |

하지만 브라우저가 **idle** 상태를 유지할 때엔, 데이터 업데이트를 감지하여 자동으로 리페치해주지 않는다.

이를 보완하기 위해서 `refetchIntervel` 옵션을 사용할 수 있다.

- 설정한 밀리초 단위로 데이터를 계속 refetching 해옴

<br/>

## 2️⃣ useMutation 훅

API 엔드포인트나 DB에 데이터를 새로 생성, 수정, 삭제

### 사용법

```jsx
const mutation = useMutation({ mutationFn: mutationFunction });
```

`mutationFn` 
- 필수 옵션.
- 실행하고자 하는 함수를 **반환**하는 함수
- 예시
  ```jsx
  const AddUser = useMutation({
      mutationFn: ( user ) => {

        return fetch('https://jsonplaceholder.typicode.com/users',
        {
          method:'post',
          headers: {
             "Content-Type": "application/json",
        },
        body:JSON.stringify( user )
      }).then( res =>  res.json() )
    })
  ```

<br/>

`반환값` 뮤테이션 실행 결과와 관련된 정보를 담은 **객체**

대표적인 **프로퍼티**

- `isLoading` 뮤테이션이 현재 로딩 중인지 여부 (boolean)
- `isSuccess` 뮤테이션 결과가 성공인지 여부 (boolean)
- `isError` 뮤테이션 결과가 오류인지 여부 (boolean)
- `data` 뮤테이션 실행 후 반환된 데이터 (있을 때만)
- `mutate` 해당 뮤테이션 실행을 위해 호출할 **메소드**. (인자에 담을 변수를 객체로 전달)
- `reset` 뮤테이션 초기 상태로 리셋하는 **메소드**
- `onSuccess` 뮤테이션 성공시 호출할 콜백함수
- `onError` 뮤테이션 실패시 호출할 콜백함수

<br/>

## 3️⃣ Query Caching

원격 서버와 통신하는데에 걸리는 시간을 단축하고자,

여러번 불러올 데이터는 캐시에 저장하여 반복해서 필요로 할 경우 원격 서버가 아닌 캐시에서 빠르게 가져올 수 있는 방식

useQuery 훅 사용 시, 지정했던 **`고유 키`** 밑에 **반환된 데이터가 캐싱**된다.

기본적으로는 캐시 데이터는 **오래된(stale) 상태**로 기록된다.

<br/>

**[ Query Caching과 관련된 useQuery 옵션 ]**

```jsx
const query = useQuery({
    queryKey: [‘users’],
    queryFn: getUsers,
    staleTime: 5000,
    cacheTime: 60000
  })
```

`staleTime` 
- xx밀리초 후에 데이터는 **stale 상태**로 처리된다.
`cacheTime` 
- xx밀리초 후에 캐시 데이터는 **가비지 컬렉션**으로 간다. (버려짐)

<br/>

## 4️⃣ Query Invalidation

지정해준 `staleTime` 과 무관하게 즉시 데이터를 stale 상태로 처리해야하는 경우가 있다.

예를 들어, API에 POST 요청을 보내 데이터 값을 업데이트할 때엔, API 엔드포인트에 있는 데이터의 값이 캐시에 저장되어있는 값보다 더 최신 상태가 되고, 캐시에 저장되어있는 데이터는 곧바로 outdated한 값이 되어버린다. 이럴 때엔 즉시 캐시 데이터를 stale 상태로 처리해줘야 한다.

> React Query의 `QueryClient` **객체**의 `invalidateQueries` **메소드** 활용

- **모든 쿼리**, 혹은 고유 키를 통해 **특정 쿼리**를 stale 상태로 처리해주는 역할

<br/>

### 사용법

- `useQueryClient` 훅을 통해 **queryClient 객체** 생성
- 객체 내장 **메소드** `invalidateQueries` 활용하기

```jsx
import { useQueryClient } from "@tanstack/react-query";

// useQueryClient 훅을 사용하여 queryClient 객체 생성
const queryClient = useQueryClient();

// 캐시의 모든 쿼리 무효화
queryClient.invalidateQueries();

// 'users'로 시작하는 키가 있는 모든 쿼리 무효화
queryClient.invalidateQueries({ queryKey: ["users"] });
```

<br/>

---
## 📌 요약

- React 훅을 사용해서 데이터를 간편하게 Fetch/Update
- 스마트 캐싱 메커니즘

→ 코드 간소화 & 성능 최적화

> React Query는 강력한 **Server State 관리 라이브러리**이다!
