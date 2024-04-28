
LLM은 오직 __ 정보만 이해할 수 있다
- 사전에 trained 된
- prompt로 명시적으로 제공된
LLM은 종종 prompt 의 전제가 사실이라고 가정
LLM은 추가적인 정보를 요청할 수 없기 때문에 사실이 아닌 정보도 제공해줄 수 있음


# Some naive solutions

![[IMG_1569.jpeg]]
## (Full) Fine-Tuning
- 데이터 준비를 위한 노력
- 높은 비용
- 실시간 학습 / 새로운 Data Update
- Still may not work

## Make Humans Check
- 시간 지연 및 높은 비용
- 휴먼 에러(신뢰할 수 없거나 부주의한 ..)

## Prompt Enginerring
- 기존 학습된 지식에 기반
- Token 수 제한
- 올바른 Context 검색이 안될 가능성 존재
- Trade off: 성능, 레이턴시, 비용


# Retrieval Augmented Generation (RAG)
`Grounding` on user data

## The Problem:
- LLM은 비즈니스의 독점 데이터 또는 도메인 특화 데이터를 알지 못함
- LLM은 실시간 정보를 가지고 있지 않음
- LLM은 정확한 인용을 제시하기가 어려움

## The Solution:
정보 검색 시스템(RAG)을 사용하여, LLM에 관련성 있는 context 실시간으로 제공

![[IMG_1570.jpeg]]



## When do you fine-tune vs RAG?
![[IMG_1571.jpeg]]


## Benefits of RAG-based workflows / applications

![[IMG_1572.jpeg]]

- Factually & Grounding: LLM이 제공할 수 있는 것 이상으로, 근거로 제시할 수 있는 정확한 증거와 출처 제공
- Better context: 일반화된 LLM의 데이터보다 더 맥락에 맞는 데이터 포함 가능
- Fresher data: LLM


## Challenges with RAG

![[IMG_1573.jpeg]]

### Quality related
- multiple hops로 인한 multiple failure modes
- workflow 및 구성요소의 품질을 측정하기 위한 tooling 필요
- Bad retrieval -> Bad results
	- Low precision: 검색된 세트의 모든 정크가 관련성이 없음
	- Low recall: 모든 관련 청크가 검색되지 않음
	- 오래된 정보 또는 중복 데이터
- Bad reponse generation: hallucination, irrelevance and toxicity/bias


## Embeddings
### Data
### DL models
### Embs(10^2~10^4 dims)

벡터라는 수치로 이산화, 여러차원 맵에 형성이 됨. 관련이 있는 군집 형성
내가 수치화 된 벡터와 구성된 벡터들 간의 가장 유사성을 찾는 것


## RAG workflow for building a QA System

### Data Ingestion / Parsing
- document(s)를 균일한 청크로 분할
- 각 청크는 raw 텍스트 조각
- 각 청크에 대한 임베딩 생성
- 각 청크를 벡터 데이터베이스에 저장

### Querying
- query 의 임베딩 생성
- 벡터 데이터베이스로부터 가장 유사한 상위 k 개 (top-k) 의 청크 찾기
- LLM 응답 합성과 연결

![[IMG_1574.jpeg]]



# Improving performance Better retrieval == better results
![[IMG_1575.jpeg]]




DEMO 튜토리얼
https://bit.ly/bwai-handson