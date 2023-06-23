(구글 개발자 컨퍼런스. 5/10 개최)

- 간판 문구 “Making AI helpful for everyone’

## SGE(Search Generative Experience)

https://youtu.be/dVsiusLQy5Q

- 생성형 인공지능이 탑재된 구글 검색
- 현재 ‘구글 실험실’에서 SGE 기능 ON/OFF 가능
- 검색UI는 그대로. 검색 결과를 보여줄 때 크롤링된 URL 링크보다 **인공지능 답변이 상단에 노출**됨
- 인터페이스 순서 : 구글 광고 → 인공지능 답변 → 검색 결과 순서
- **‘Ask a follow-up’** 누르면 프롬프트로 추가 질문 가능
- 현재 구글 매출의 약 80%가 광고 매출이어서, 추후 인공지능 답변 내용에도 광고 BM을 넣을 수 있음
- 기존 SEO(검색엔진최적화) 상단 노출 경쟁이 더 치열해질 것으로 예상. 또 검색엔진 외에도 **인공지능 답변에 노출될 수 있는 최적화 방식**에 대해서도 새롭게 논의될 수 있음

## PaLM2

- 2022.04에 공개된 PaLM의 다음 세대 (구글의 언어 모델)
- Fine Tuning 성능 강조
  - Med-PaLM2 : 헬스 케어 특화 모델 (RLHF 방식으로 강화)
  - Sec-PaLM2 : 보안 분야 특화 모델
- 독보적인 **매개변수** 5,400억 개
  - GPT3.5의 매개변수 1,750억 개
  - 메타 라마의 매개변수 650억 개
- PaLM2 기반으로 **Bard**(구글 인공지능 챗봇) **활용성 향상**
  - 100개 이상의 다국어 학습
  - 수학 및 추론 능력 향상
  - 코딩 가능
- 모델 제품군 (크기 오름차순)
  - Gecko : 모바일 디바이스에서 작동할 정도로 작음 . 오프라인 상태로 사용 가능
  - Otter
  - Bison
  - Unicorn

→ 모델 종류/규모가 다양해짐에 따라 사용자가 **VertexAI**(구글 머신머닝 도구)**에서 파인튜닝** 용이

### Bard

- 구글 AI 챗봇
- **대상 언어** 확대 (영어 ⇒ 180개국 40개 이상의 언어)
  - 한국어도 포함됨 (네이버, 카카오 모델과 경쟁 예상)
- **코딩** : 20개 이상의 프로그래밍 언어로 코딩,디버깅,코드 설명 가능
  - Colab, Replit에 내보내기 가능
- **구글 도구 연동** : 구글 검색, 구글 렌즈(이미지 검색), 구글 맵 연동됨
- **워크플로우 강화**를 위한 연동성 향상
  - 구글 독스, 구글 시트, 지메일로 내보내기 가능
  - like ChatGPT Plugins

## Duet AI for Google Workspace

- **Gmail - Help me write**
  - 프롬프트에 내용 입력하면 맥락에 맞게 메일 작성
- **Google Docs - Help me write**
  - 프롬프트에 내용 입력하면 본문 생성
<div>
  <img width="450px" src="https://github.com/lydiacho/TIL/assets/81505421/dc07d441-8998-49e1-bb50-66c3d768c049"/>
  <img width="450px" src="https://github.com/lydiacho/TIL/assets/81505421/765eee0f-55eb-4943-9ec0-c65f249ab6b6"/>
</div>

- **Google Sheets - Help me organize**
  - 프롬프트에 내용 입력하면 표 생성
![image-11](https://github.com/lydiacho/TIL/assets/81505421/6c849d3a-e7f3-465f-a4f2-5b334b0ddeea)

- **Google Slides - Help me visualize**
  - 프롬프트에 내용 입력하면 이미지 생성
  - **슬라이드별 발표 대본 작성해주는 기능 추가**
 
![image-12](https://github.com/lydiacho/TIL/assets/81505421/31b65741-9db2-489c-b0dc-4fad352d594f)

### Sidekick 기능

- 문서 내용과 작업 맥락을 파악해 다음 단계에 적합한 프롬프트 질문을 추천해주는 기능
- 질문에 대한 질문,원하는 내용을 도출하기 위해 프롬프트에 무엇을 입력해야 할지 고민하는 경우에 대한 솔루션
- Google Docs, Sheets, Slides에 적용
