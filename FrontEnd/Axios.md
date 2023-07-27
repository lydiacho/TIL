# Axios 서버 통신과 API 연동


## Axios

- 내장함수인 fetch를 사용하지 않고 간편화해주는 서버통신 라이브러리
- response body를 문자열 형태로 주는 fetch와 달리 JSON 형태로 주기 때문에 별도로 `.json()` 변환을 해주지 않아도 된다.

- axios와 fetch의 차이를 알아두자!

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7bc9d750-46f2-4c86-a264-d7613afa2e18/Untitled.png)

## Axios의 메소드 종류

- axios.**get**(url[, config]) : 데이터 가져오기
- axios.**delete**(url[, config]) : 데이터 삭제
- axios.**post**(url, **data**[, config]) : 데이터 등록하기
- axios.**put**(url, **data**[, config]) ; 데이터 갱신(수정)하기
    - 서버 내부적으로 get → post 과정을 거침
    - **모든 내용** 덮어쓰는 개념
- axios.**patch**(url, **data**[, config]) : 데이터를 수정하고자 서버에 요청 보낼 때
    - **필요한 부분만** 수정하는 개념

## Axios 서버 통신의 기본 형태

- response라는 객체의 내부 property 종류
    - config, data, headers, request, status, statusText 등..
- 우리가 얻고자 하는 응답 데이터는 `response.data`로 접근
- get 통신
    
    ```jsx
    axios.get(`https://example-url.com/user/123`, { headers: { 헤더키: '헤더값' } });
    ```
    
- post 통신
    
    ```jsx
    axios.post(
      `https://example-url.com/user`,
      { requestBody키: 'request-body-값' },
      { headers: { 헤더키: `헤더값` } },
    );
    ```
    

하지만 대개 한 프로젝트 내에서 

- baseURL
- headers

이 두가지는 공통적으로 사용되기 때문에 별도로 설정해줌으로써 코드의 반복을 줄일 수 있다. 

## axios.create()

create 메소드를 사용해서 기본값을 세팅해보자. 

```jsx
export const custom = axios.create({
	baseURL: 'https://example-url.com',
	headers: {헤더키 : '헤더값'}
});

custom.get('/user/123');
custom.post(
	'/user',
	{ id: 123, name: '김뫄뫄' }
);
```

- 이렇게 baseURL과 headers를 create 메소드로 별도 설정해주고,
- 사용할 때엔 `axios` 키워드를 create 메소드를 정의한 **함수명**(위에선 `custom`)으로 대체하여 사용하면 된다.

또, create 메소드를 사용하는 함수 (위의 코드에서는 `custom`)을 별도의 파일로 분리하는 경우가 많다. 

(보통 `lib` 디렉토리에 넣어놓음)

---
### 참고문헌 

https://react.vlpt.us/integrate-api/01-basic.html

[https://velog.io/@seondal/React-Query-Axios로-쉽게-서버통신하기](https://velog.io/@seondal/React-Query-Axios%EB%A1%9C-%EC%89%BD%EA%B2%8C-%EC%84%9C%EB%B2%84%ED%86%B5%EC%8B%A0%ED%95%98%EA%B8%B0)

https://velog.io/@yrats/Axios