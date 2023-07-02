## For what? ⇒ 자동 슬라이드 (Carousel)

- 자동으로 슬라이드
- 슬라이드 넘어가는 속도, 머무르는 속도 커스텀
- pagination bullet 커스텀 (색상 변경)
- loop 옵션 (마지막페이지에서 첫번째페이지로 자연스럽게 이동, 무한반복)

> **💡 sol) `swiper` 라이브러리**

### ✔️ 사용방법

1. **설치 : `yarn add swiper`**
2. **기본적인 Swiper 사용을 위한 import**
   - `import { Swiper, SwiperSlide } from "swiper/react";`
   - `import 'swiper/css';`
3. **추가적인 Swiper 모듈 사용을 위한 import**

   `Autoplay` : for 자동슬라이드

   `Pagination` : for 하단 indicator (bullet)

   - `import { Autoplay, Pagination } from 'swiper';`
   - `import 'swiper/css/pagination';`

4. **기본적인 UI 배치**

   1. 상단 요소 : `Swiper`

      → **사용한 option**

      - `modules` : 추가 기능에 필요한 모듈
      - `pagination` : indicator 클릭을 통한 페이지 이동 가능 여부
      - `slidesPerView` : 한 슬라이드 당 보여줄 요소 개수

      > 그 외 무수히 많은 옵션은 **공식 문서** 참고 ! https://swiperjs.com/react

   2. 내부 요소 : `SwiperSlide`

   ```tsx
   <div className="swiper_container">
     <Swiper
       modules={[Autoplay, Pagination]}
       pagination={{ clickable: true }}
       slidesPerView={1}
     >
       <SwiperSlide>
         <div className="one_card">Slide 1</div>
       </SwiperSlide>
       <SwiperSlide>
         <div className="one_card">Slide 2</div>
       </SwiperSlide>
       <SwiperSlide>
         <div className="one_card">Slide 3</div>
       </SwiperSlide>
       <SwiperSlide>
         <div className="one_card">Slide 4</div>
       </SwiperSlide>
     </Swiper>
   </div>
   ```

   ### ✔️ Pagination

   `Pagination` : 하단의 indicator (bullet) 사용을 위한 module

   css를 조금만 건드려도 Bullet이 사라지는 문제에 쉽게 봉착하게 된다.

   → Bullet의 **position이 absolute**로 설정되어있기 때문!

   → position을 풀어줌과 동시에 다양한 **css 커스텀**을 위해 className을 파고들어야 한다.

   #### **Pagination Bullet의 상단 class명 : `swiper-pagination`**

   > ⚠️ **주의!**
   > 그냥 .swiper-pagination에 css를 주면 아무런 적용이 되지 않을 것이다.
   > 그럴 땐, 현재 나의 css 파일이 라이브러리의 css 파일을 덮어쓸 수 있도록 import를 배치하자.
   >
   > ```
   > // import "./App.css"; -> 원래 여깄었음
   > import "swiper/css";
   > import "swiper/css/pagination";
   > import "./App.css";
   > ```
   >
   > - 이 외에 className보다 우선순위인 id를 지정해서 스타일을 주는 등 다양한 해결책이 있다.
   >   https://think0wise.tistory.com/24 → 참고!

   #### 각 Bullet의 class명 : `swiper-pagination-bullet`

   그중에서도 현재 나타나는 슬라이드에 해당하는 bullet은 `swiper-pagination-bullet-active`

   따라서 기본 파란색의 bullet **색을 수정**하고 싶을 땐 아래와 같이 지정해주면 된다.

   ```css
   .swiper-pagination-bullet.swiper-pagination-bullet-active {
     background-color: pink;
   }
   ```

   ![스크린샷 2023-07-01 오후 8.24.51.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/533ddf60-645f-4383-aad2-e8d8ee8b2312/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-07-01_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_8.24.51.png)

### ✔️ Autoplay

- 슬라이드를 자동으로 넘기고 싶을 땐

```
autoplay={{
            delay: 2000,
          }}
```

- `delay` : 각 슬라이드당 머물 시간 (ms 단위 - 2초동안 머무르도록 설정)

### ✔️ 페이지 무한 반복

- Slider에 `loop={true}` 옵션 추가

### ✔️ 슬라이드 속도 조절

- Slider에 `speed={2000}` 옵션 추가 (ms 단위 - 넘기는 시간을 2초로 설정)

## 구현 결과물

![ezgif.com-video-to-gif-17.gif](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a4ba4039-e720-4ecb-940f-16917c25813e/ezgif.com-video-to-gif-17.gif)
