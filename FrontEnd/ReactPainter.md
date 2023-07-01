# 캔버스 그림 그리기 기능 구현

사용한 라이브러리 : **`react-painter`**

```jsx
import { ReactPainter } from "react-painter";
```

1. `div` : 캔버스 Wrapper
2. `ReactPainter` : 라이브러리에서 제공하는 컴포넌트
   - `width`, `height` 지정 가능
   - `onSave` : 캔버스 저장 시 실행할 함수
     - 인수로 들어오는 `blob`을 `createObjectURL`로 넘겨서 이를 src로 가지는 img 생성하기
   - `render` : 실제 캔버스 뷰를 뱉어주는 아이
     **🔽 쓸만한 인수** (라이브러리가 제공)
     - `setColor` : 붓 색깔 설정
     - `setLineWidth` : 붓 크기 설정
       **🔽 className에 따라 어떤 역할 하는 친구들인지 설명**
     - `color_Btn` : 펜 색 설정 버튼
     - `input (type=”color”)` : 버튼으로 만든 특정 색 외에 다양한 색을 선택할 수 있는 컬러팔레트
     - `input (type=”range”)` : 붓의 크기를 정할 수 있는 range 바
   - `button ‘save’` : 완성된 캔버스 그림을 저장하는 함수(triggerSave) 실행

- 실제 구현했던 코드 (설명에 불필요한 코드*`ex-스타일`* 등 다 지운 상태)

  ```jsx
  <div>
    <ReactPainter
      width={200}
      height={270}
      onSave={(blob) => {
        imgsrc = URL.createObjectURL(blob);
        // 필요한 곳에서 imgsrc를 src로 가지는 img 태그 박는 코드
        modalClose();
      }}
      render={({
        getCanvasProps,
        triggerSave,
        canvas,
        setColor,
        setLineWidth,
      }) => (
        // 본격적인 캔버스 뷰
        <div>
          <div>{canvas}</div>
          <div>
            <button
              className="color_Btn"
              style={{ backgroundColor: "#cc5959" }}
              onClick={() => setColor("#cc5959")}
            ></button>
            <button
              className="color_Btn"
              style={{ backgroundColor: "#530e80" }}
              onClick={() => setColor("#530e80")}
            ></button>
            <button
              className="color_Btn"
              style={{ backgroundColor: "#93c47d" }}
              onClick={() => setColor("#93c47d")}
            ></button>
            <button
              className="color_Btn"
              style={{ backgroundColor: "#8da2bc" }}
              onClick={() => setColor("#8da2bc")}
            ></button>
            <button
              className="color_Btn"
              style={{ backgroundColor: "#ffc16f" }}
              onClick={() => setColor("#ffc16f")}
            ></button>

            <input
              className="input"
              type="color"
              onChange={(e) => setColor(e.target.value)}
            />

            <input
              type="range"
              onChange={(e) => setLineWidth(e.target.value)}
            />
          </div>

          <div>
            <button
              onClick={() => {
                triggerSave();
              }}
            >
              Save
            </button>

            {/* 모달 close 버튼 생략*/}
          </div>
        </div>
      )}
    />
  </div>
  ```

**🔽 자료 참고**

[GitHub - aml2610/react-painter: React component for drawing on canvas with 0 dependencies](https://github.com/aml2610/react-painter)
