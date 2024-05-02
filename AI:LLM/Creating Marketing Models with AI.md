# 개요
The GenAI Era
Marketing Mix Model
Marketing Mix Model+Gemini Use Case

# LLM 3인방
`Gemini vs ChatGPT vs Claude`


# LLM이 주목받는 이유
1. LLM은 기존의 소규모 모델에서 시도할 수 없었던 작업을 수행하는 새로운 능력을 보임
2. 인간 언어에 대한 LLM의 문맥 이해 능력을 통해 우리의 데이터 및 지능형 시스템과 상호 작용하는 방식이 변화
3. LLM은 대규모의 이질적인 데이터에서 패턴과 연관성을 찾을 수 있음

# Gemini

## Multimodality

![[IMG_1563.jpeg]]


데이터의 결과를 전달할 때 결국 이미지와 텍스트를 함께 전달.
텍스트만 가지고 텍스트를 뽑거나 이미지를 가지고 이미지를 뽑는 것은 한계
이미지와 텍스트를 넣어서 같이 활용한다면 효율적


## AI 활용안의 발전방향
### Predictive AI
회귀 및 분류, 예측 분석, 감정 분석, 특성 추출, 객체 파악, ...
### Generative AI
텍스트, 이미지, 코드 생성, 텍스트 및 코드 재작성 및 형식화 요약, 이미지 ,비디오 내용 서술 Q&A 내용 생성, ...
### Multimodal Generative AI
일반 이미지 이해, 공간적 추론 및 논리, 시각적 내용에 대한 수학적 추론, 영상 질문에 대한 답변, 자동 음성 인식 및 통역, ...



# Marketing Mix Model
## 마케팅 환경의 변화
- 브라우저에서 타사 쿠키를 사용하지 못하게 됨
- 보다 강력한 데이터 개인정보 보호 규정이 시행
`기존의 어트리뷰션 기반 마케팅 성과 측정 및 개별 사용자 수준 데이터 추적이 어려워짐`


## Marketing Mix Model(MMM)
`Model` `Analyze` `Optimize`
마케팅 활동을 통해 얼마나 많은 비즈니스 결과(예:매출)가 발생하는지를 파악하는 방법으로, 투자 대비 수익(ROI) 측면에서 마케팅의 효과를 평가하고 이를 활용하기 위해 만들어진 계량경제학적 접근법

## 현대적 MMM 주요 접근 방식

| 만든 곳  | Google (Lightweight MMM)                         | Meta (ROBYN)                                                      | Uber (Orbit)                                  | Sass 공급업체 (Third Party MMM)          |
| :---- | ------------------------------------------------ | ----------------------------------------------------------------- | --------------------------------------------- | ------------------------------------ |
| 성격    | 오픈소스 MMM 라이브러리(Python)                           | 오픈소스 MMM 패키지 (R, Python(beta))                                    | 오픈소스 시계열 분석 라이브러리 (Python) 활용한 접근             | 업체별 소프트웨어, 웹서비스 등                    |
| 활용 특징 | 1. 베이지안 확률 모델링 활용<br>2. Numpyro와 JAX를 활용한 빠른 모델링 | 1. 동적 모델링<br>2. 실시간 캠페인 최적화<br>3. 크로스 채널 통합 기능 등<br>4. Prophet 활용 | 1. 베이지안 확률 모델링 활용<br>2. Stan와 Pyro 등을 통합해서 사용 | 1. 일정한 결과, 안정성 보장<br>2. 소프트웨어 유지보수 등 |


## LightWeightMMM
- MMM에 베이지안 접근 방식을 사용하여



# MMM 실습 Training

![[MMM실습.mov]]

## 기본 실행 내역
### Loading Data
- GCP 인증 후 SQL 사용해서 BigQuery에서 데이터를 가지고 옴

### Raw Data
- 일별 브랜드와 광고 내역 관련된 데이터가 기록되어 있음

### Preprocessing Data
- 데이터를 날짜와 AdGroup 기준으로 집계하고 이상치 처리

### Scaling Data
- 특정 시간을 기준으로 이전까지의 광고 데이터를 훈련 데이터로, 이후 데이터를 검증 데이터로 구분
- 평균을 기준으로 데이터를 축소함
- 모델에 대입할 숫자값으로 변환

### Prediction Model Fitting
- 인과 관계 합성곱을 적용하여 먼 값보다 가까운 값에 더 많은 가중치를 부여하는 모델
- Model fitting
- Prediction
- 3개의 모델에 대해 각각 3개의 degree를 넣어 확인 결과 MAPE(평균 절대 비율) 확연하게 적은 모델과 비교

### Plotting
- LightweightMMM에서 자체 그래프 기능 지원 (pandas 기반 선/막대 그래프)

### Budget Optimizer

### Understanding Data with Gemini
- 데이터에 대한 간단한 배경과 활용 용도 설명 후 EDA 및 outlier 정보 요청

### Plotting Description with Gemini
MMM에서 만든 결과 그래프에서 대한 배경 지식을 재공한 후 해당 그래프를 읽고 이에 대해서 설명하고 인사이트를 찾아 내재화됨


# Further Action Items; 추가 조치 항목

- Meridian 접근 가능할 때 까지 기다린다.
- AI 연계 추가
	- 더 쉬운 모델 선택
	- 매개변수 조정 등을 사용자가 직접 할 수 있다는 방안 고안
	- 보다 상세한 데이터 정제 방안 제시 방법 등
- 타 라이브러리 기능에 AI 연계
- 타 분야의 더 쉬운 데이터 활용을 위한 AI 연계고민
- 각자의 분야 개선
	- 초심자나 각자의 분야에서 잘 모르는 사람들을 위한 AI 활용 방안 고안
	- 작은 것부터 이야기하고 시작해보기