# set 자료구조

- 고유한 값들의 집합을 다루는 자료구조
- 순서 X, 중복 X

▶️ **배열과의 차이점**

- 배열 :
  - 순서O : 인덱스를 통해 특정 위치의 데이터에 접근 가능
  - 중복O : 값이 같아도 인덱스가 다르기 때문에 문제 없음
- 세트 :
  - 순서X : 인덱스 통해서 데이터 접근 불가능
  - 중복X : 중복된 값 추가하면 아무 일도 일어나지 않음

**▶️ set 생성**

- JS에서 Set은 class의 일종이다 → `new` 키워드 사용해서 생성해야 함

```jsx
const s1 = new Set(); // size : 0
const s2 = new Set(2); // size : 2
const s3 = new Set([1, 2, 3]); // Set(3) {1,2,3}
```

- 생성자 인자
  - 빈값 : 사이즈 0 세트 생성
  - 정수 : 사이즈 n 세트 생성
  - 배열 : 배열 요소로 이루어진 세트 생성

**▶️ set 에 값 추가**

- 메서드 : **add()**
- 특정 값 추가

```jsx
set.add(1);
set.add("A");
set.add(true);

// 연쇄 적용도 가능
set.add(1).add("A").add(true);
```

- 중복된 값을 또 넣으면 아무 효력 없다

**▶️ set 에서 값 삭제**

- 메서드 : **delete()**
- 특정 값 삭제
- 반환값
  - 삭제에 성공 : true
  - 삭제에 실패 (값이 세트에 존재X) : false

```jsx
set.delete(1);
```

**▶️ set 에서 값 존재 여부 확인**

- 메서드 : **has()**
- 조건문이나 삼항 연산자와 함께 많이 쓰임

```jsx
if (set.has(1)) {
  // 블라블라
}

const result = set.has(1) ? "있음" : "없음";
```

**▶️ set 에서 값 개수**

- 속성 : **size**

```jsx
console.log(set.size);
```

**▶️ set 의 모든 값 제거**

- 메서드 : **clear()**

```jsx
set.clear();
```

**▶️ set 순회**

- **for … of** … 로 자주 쓰임

```jsx
for (const i of set) {
  console.log(i);
}
```

- **forEach**도 가능

```jsx
set.forEach((i) => console.log(i));
```

**▶️ 배열 ↔ set 변환**

- 배열 → set
  - new Set 생성자의 인자로 배열 넣어주기
  - **중복값이 제거된다**
  ```jsx
  const set = new Set(arr);
  ```
- set → 배열
  - 스프레드 연산자 사용
  ```jsx
  const arr = [...set];

  // 혹은 아래의 방법도 있음
  const arr = Array.from(set);
  ```

**▶️ set 활용해서 배열에서 중복 값 제거**

- set만 거치면 배열 중복값을 편리하게 삭제 가능
  - **배열 → set으로 변환 → 배열로 변환**

```jsx
const arr1 = [1, 1, 1, 2, 2, 2];
const arr2 = [...new Set(arr1)];
```

**▶️ set로 집합 연산**

- 합집합
  ```jsx
  const union = new Set([...set1, ...set2]);
  ```
- 교집합
  ```jsx
  const intersection = new Set([...set1].filter((i) => set2.has(i)));
  ```
- 차집합
  ```jsx
  const difference = new Set([...set1].filter((i) => !set2.has(i)));
  ```
