
```
# part 4. 머신런닝 기반 데이터 분석

# 3. 의사결정 나무
# 2)데이터 분할 #page159
# ① iris 데이터 셋을 이용하여 train data에서 70%, test data에 30% 랜덤하게 분할한다.
data(iris) # iris 데이터 셋 불러오기
head(iris);tail(iris) # 데이터 앞6행, 뒤6행을 동시에 확인하기
names(iris)<-tolower(names(iris)) # 변수를 소문자로 변경하기
idx<-sample(1:nrow(iris),nrow(iris)*0.7) # sample()함수로 7:3으로 분할하기
train<-iris[idx,] # train으로 70%의 iris 데이터셋 랜덤 배정하기
test<-iris[-idx,] # test으로 30%의 iris 데이터셋 랜덤 배정하기

# ② 데이터 분할 확인하기
nrow(train)

nrow(test)



# 8) rpart 패키지를 이용하여 iris data 의사결정나무 분석 #page163
# ① rpart()함수 이용 의사결정나무 생성

# ② 패키지 설치 및 설치
install.packages("rpart")
library(rpart)

# ③ 데이터로딩(Loading)
data(iris) # iris data를 불러온다.
colnames(iris)<-tolower(colnames(iris))# 분석 효율성을 위해 변수명 모두 소문자로 변경한다.

# ④ rpart() 함수 이용 분류분석
k<-rpart(species~.,data=train) # rpart함수는 사용 방법(종속변수~ 설명변수, 데이터명)
k # 학습된 결정 트리에 대한 정보를 확인할 수 있다.

# ⑤ rpart()시각화
install.packages("rpart.plot")
library(rpart.plot)
prp(k,type=4,extra=2,digits = 3)

# ⑥ 해설

# ⑦ train data의 모델 평가
p<-predict(k,train,type='class')
table(p,train$species)

# ⑧ test data 분류 예측하기
t<-predict(k,newdata=test,type='class')
table(t,test$species)



# 4. 랜덤포레스트(Random Forest) #page167
# 2) randomForest 패키지를 이용하여 iris data 분석
# ① randomForest()함수

# ② 패키지 설치 및 로딩
install.packages("randomForest")
library(randomForest)

# ③ 데이터 로딩(Loading)
data(iris) # iris data를 불러온다.
colnames(iris)<-tolower(colnames(iris))# 분석 효율성을 위해 변수명 모두 소문자로 변경한다

# ④ randomForest() 함수 이용 모델 생성
library(randomForest)
m1<-randomForest(species~.,data=train)
m1

# ⑤ 해설

# ⑥ 중요변수 보기
varImpPlot(m1)



# 5. 인공신경망(Artificial Neural Network)
# 3) neuralnet 패키지를 이용하여 iris data 분석 #page170
# ① neuralnet()함수

# ② 패키지 설치 및 로딩
install.packages("neuralnet")
library(neuralnet)

# ③ 데이터 로딩(Loading)
data(iris) # iris data를 불러온다.
colnames(iris)<-tolower(colnames(iris))# 분석 효율성을 위해 변수명 모두 소문자로 변경한다.

# ④ 수치형으로 컬럼 생성 #page171
train$species2[train$species=='setosa']<-1
train$species2[train$species=='versicolor']<-2
train$species2[train$species=='virginica']<-3
train$species<-NULL # 기존 칼럼 제거
head(train)

# ⑤ 데이터 정규화
normal<-function(x){
  return((x-min(x))/(max(x)-min(x)))
}

train_nor<-as.data.frame(lapply(train,normal))

summary(train_nor)

# ⑥ 인공신경망 모델 생성 #page172
m3<-neuralnet(species2~.,data=train_nor,hidden=1)
m3

plot(m3)

# ⑦ 분류 모델 성능 평가
m4<-compute(m3,train_nor[c(1:4)])
m4$net.result

```