
# Goals
- LLM 을 확장성있게 Serving 하는 법
- Cloud 환경에서 Model을 배포하기 위해 필요한 요소
- Model 을  Deployment할 수 있는 플랫폼

# How to deployment softwares well?
SLDC: Software Development Life Cycle

# How to deployment models well?
어떻게 모델을 효율적이게 관리하고 배포하는지?

- Data Gathering
- Model Training
- **Model Deploy**
	- 모델을 환경에 노출시켜 사용하는 방법
- Model Maintenance

# Model Deploy 를 잘하는 법

## Model Development Platform

Self-Hosted <-> Fully-Managed

**"Manged Kubernetes(관리형 쿠버네티스)"**

![[IMG_1542.jpeg]]

## Kubernetes Platform
### How Kubernetes Works?

![[IMG_1543.jpeg]]



# Why Kubernetes for LLM Deployment?
1. Scalability(확장성)
	1. Container Scaling, GPU Node Scaling; 컨테이너 스케일링, GPU 노드 스케일링
2. portability(휴대성)
	1. Container-based Workload; 컨테이너 기반 워크로드
3. Flexibility(유연성)
	1. Broad ecosystem, Tools; 광범위한 에코 시스템, 도구


# Managed Kubernetes Service
관리형 쿠버네티스를 사용하는 추세.
그 이유는 쿠버네티스를 설정하는 소요값이 너무 크다.
관리형 서비스를 사용해서 어려운 관리나 배포를 다른 요구를 신경쓰지 않고 온전히 집중하게 해줌


# LLM Deployment Architecture

![[IMG_1546.jpeg]]

## Kubernetes Cluster
Types of Google Kubernetes Engine
### GKE Standard
- 노드 구성, 온전히 배포
### GKE Autopilot
- standard 포함. 노드의 대한 운영까지

### LLM Model on GKE
GPU Accelerator
GPU Driver
COS Image
Virtual Machine


## GPU
H100
A100
L4
T4

### Requirements for GPUs in Kubernetes

![[IMG_1548.jpeg]]

Device plug-in
OS Requirements
Container Requirements
GPU Sharing
GPU Monitoring
...
And many things..

#### GPU in GKE
1. Support GPU Sharing Strategy
2. Builds-in GPU Driver
3. Monitoring GPU


### Requirements for LLM Gateway

☑️ **Single Endpoint**
- 항상 단일한 진입점을 제공
- Address mapping
☑️ **Load Balancing**
- Autoscaling
- Session affinity
☑️ **Traffic Management**
- Path based routing
- Protocol translation


## Choose your Load Balancer

![[IMG_1550.jpeg]]


## Cloud Load Balancer Features
1. L7,L4 Support
	1. HTTP(S), HTTP/2, HTTP/3, TCP, UDP
2. Balancing algorithm
	1. Weight-based, Hash-based, Closest region, Round-robin
3. Additional features
	1. WAF, SSL Offloading, Session affinity, Autoscaling


## Requirement for LLM Storage

☑️ **Format**
- Extensibility
- Metadata & Binary
☑️ **Storage**
- Scaling
- Partitioning
☑️ **Discoverability**
- Index
- URL Endpoint
☑️ **Security**
- ACL
- Authorization

**;Format**
- 스토리지의 포맷이 호환성이 좋고 일반적이야 함.
- 모델이 스토리지에 이동하거나 동시 보관할 때 굉장히 많은 요소를 둠


### OCL Image Spec
컨테이너 이미지를 위한 규격이지만
패키지나 LLM 모델 같은 다양한 범위까지 포맷에 대한 호환성이 잘 유지되는 스토리지

![[IMG_1553.jpeg]]

### Google Cloud Artifact Registry
1. OCI Compliant
	1. Support OCL format
2. Security features
	1. RBAC (Role Based Access Control)
3. Endpoint
	1. Provide Registry URL


## Autoscaler

### Auto Scalers in GKE

![[IMG_1555.jpeg]]

1. HPA(수평확장)
2. VPA(수직확장)
3. MPA(수평-수직 확장을 결합해서 동시에 두가지 확장을 사용)
4. CA(클러스터 노드의 확장)
5. NPA(노드 풀 단위로 수평확장을 할 수 있는 기능)


## Model Scaling
`need more!`
Model containers
GPU Nodes


# Google Cloud LLM Architecture

![[IMG_1556.jpeg]]


# Deployment LLM with Gemma

## Gemma
Open source, Light-weight Model
1. Cost-efficient
2. Fast deployment
3. Cross-device Compatibility
-> Works well with Kubernetes!


## Deployment Planning

![[IMG_1558.jpeg]]

1. Get Model
2. Prepare GPU Model
3. Deploy Model

### 1. Get Model

![[IMG_1559.jpeg]]

Get Gemma with vLLM Image
1. Get Public Image
2. Create custom model
3. Push to Private Registry

### 2. Prepare GPU Nodes
Calculating the amount of GPUs

`Parameters count X Bits = Required GPU Memory`

Example: Gemma-2b Model

`w2 Billion Params X 4 Bits = 8GB`

-> Require 8GB Memory GPU at minimum

#### Create Node with CPU
필요한 만큼 GPU Count, Type을 쉽게 생성

### 3. Deploy Model

![[IMG_1561.jpeg]]


# DEMO Training

![[LLM배포실습.mov]]

