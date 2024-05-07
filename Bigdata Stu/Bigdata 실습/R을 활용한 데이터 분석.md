```R
# CSV 파일 불러오기
data <- read.csv(“C:/data/Data1.csv”, header=TRUE, sep=“,”)


벡터로 변수 선택하기
test <- data[c(1:22)]
test
# View(test)

# 새변수 만들기
# 데이터프레임명$변수명을 사용하는 방법
test$BF <- (test$Q1 + test$Q2 + test$Q3 + test$Q4 + test$Q5) / 5

# attach 함수를 사용하는 방법
attach(test)
test$BM <- (test$Q6 + test$Q7 + test$Q8 + test$Q9 + test$Q10) / 5
detach(test)



# transform 함수를 사용하는 방법
attach(test)
test <- transform(test, Happiness = (Q11 + Q12 + Q13 + Q14 + Q15) / 5)
detach(test)

#그룹변수 만들기
① 평화변수 만들기
attach(test)
test$Peace <- (Q16 + Q17 + Q18 + Q19 + Q20) / 5
detach(test)

② 평화변수의 분할표
table(test$Peace)
prop.table(table(test$Peace))
table(test$Peace)

③ 평화변수를 3집단으로 분류
attach(test)
test$grp.Peace[Peace >= min(Peace) & Peace <= 3.2] <- 1
test$grp.Peace[Peace >= 3.3 & Peace <= 3.8] <- 2
test$grp.Peace[Peace >= 3.9 & Peace <= max(Peace)] <- 3
detach(test)
table(test$grp.Peace)

# 새 변수로 재부호화하기
attach(test)
test$Gender[Gender1 == 10] <- 1   # 남자
test$Gender[Gender1 == 20] <- 2   # 여자
detach(test)
table(test$Gender)

# 변수의 방향을 역으로 재부호화 하기
attach(test)
test$EDU[EDU1==4] <- 1
test$EDU[EDU1==3] <- 2
test$EDU[EDU1==2] <- 3
test$EDU[EDU1==1] <- 4
detach(test)
table(test$EDU)

# 두 독립변수의 변수값을 교차시켜 하나의 집단변수 만들기
attach(test)
test$grp.Gender.Peace[Gender==1 & grp.Peace==1] <- 11
test$grp.Gender.Peace[Gender==1 & grp.Peace==2] <- 12
test$grp.Gender.Peace[Gender==1 & grp.Peace==3] <- 13
test$grp.Gender.Peace[Gender==2 & grp.Peace==1] <- 14
test$grp.Gender.Peace[Gender==2 & grp.Peace==2] <- 15
test$grp.Gender.Peace[Gender==2 & grp.Peace==3] <- 16
detach(test)

# 결측값 지정하기
test$Gender[test$Gender == 99] <- NA
test$EDU[test$EDU == 99] <- NA
table(test$Gender); table(test$EDU)
sum(test$EDU); sum(test$EDU, na.rm=TRUE)
# summary(test$Gender); summary(test$EDU)

# 결측값 제거하기
test <- test[complete.cases(test),]

# 데이터 병합하기
# 변수를 병합하는 경우
data$ID <- seq.int(nrow(data))
data1 <- data[,c(27, 21, 22, 23)]
data2 <- data[,c(27, 24, 25, 26)]
str(data1); str(data2)
mergedata <- merge(data1, data2, by=“ID”)
str(mergedata)

# 데이터 분할하기
# 일부 변수를 추출하는 경우
# data의 첫 세 변수만 추출하는 경우 1
newdata <- data[,c(1:3)]
newdata

# data의 첫 세 변수만 추출하는 경우 2
var <- c(“Gender1”, “EDU1”, “BF”)
newdata <- data[var]
newdata

# 일부 사례만 선택하는 경우
# data의 처음 5개 사례만 추출하는 경우
newdata <- data[1:5,]
newdata

# 남자만 선택하는 경우
newdata <- data[which(data$Gender==10),]
newdata

# 남자 중에서 평화 정도가 낮은 경우만 선택하는 경우
newdata <- data[which(data$Gender==10 & data$Peace <= 3.2),]
newdata

# subset 함수를 사용하여 사례와 변수를 추출하는 경우
newdata <- subset(data, Happiness>=3 & Peace >= 3, select = c(“Gender1”, “EDU1”, “BF”, “BM”, “Happiness”, “Peace”))




# 변수의 이름과 레이블 설정
# names() 변수 이름을 모두 출력하는 함수
names(test1)

# 특정 변수 이름을 변경할 때(변수 이름 기준)
names(test1)[names(test1)==“Happiness”] <- “test_Happiness”
names(test1)

# 특정 변수 이름을 변경할 때(위치 기준)
colnames(test1)[1] <- “new_Gender”  # 1번째 column 변수명을 변경

# 전체 변수 이름을 지정하여 변경할 때 변수의 개수와 이름의 개수가 같아야 한다.
abc <- c(“Q11”, “Q12”, “Q13”)
mydata <- data[abc]
mydata 
names(mydata) <- c(“apple”, “banana”, “cherry”)




# table 함수를 이용한 빈도표 출력
table(test$EDU)


# plyr 패키지를 이용한 빈도표 출력
install.packages(“plyr”)
library(plyr)
count(test, ‘EDU’)

# 기술 통계량 출력
# summary 함수를 이용한 기술통계량 출력
summary(test$EDU)

# psych 패키지를 이용한 기술통계량 출력
install.packages(“psych”)
library(psych)
describe(test$EDU)



# 교차분석
# 대립가설: 성별에 따라 전반적인 평화의 분포가 다를 것이다.
# table 함수를 이용한 교차분석
① 평화 변수값을 새 변수명으로 재부호화 한다.
② 재부호화한 새 변수의 변수값 설명을 입력한다.
③ 두 변수의 값에 따른 사례수를 계산한다.
④ 두 변수의 값에 따른 주변 합계를 계산한다.
⑤ 두 변수의 값에 따른 비율을 계산한다.
⑥ 카이제곱분포를 계산한다.
# Peace 속성을 ‘낮음’ ‘보통’ ‘높음’ 응답으로 재부호화
# 앞장에서 ‘재부호화’를 통해 해당 변수를 만들어 놓았음
# attach(test)
# test$grp.Peace[Peace >= min(Peace) & Peace <= 3.2] <- 1
# test$grp.Peace[Peace >= 3.3 & Peace <= 3.8] <- 2
# test$grp.Peace[Peace >= 3.9 & Peace <= max(Peace)] <- 3
# detach(test)
# table(test$grp.Peace)



# 두 변수의 값에 따른 사례수 출력
devi02_1.re <- table(test$grp.Peace, test$Gender)
devi02_1.re

# 변수값을 변수값 설명으로 대체
attach(test)
test$grp.Peace_1[grp.Peace==1] <- “1_평화 낮음”
test$grp.Peace_1[grp.Peace==2] <- “2_평화 보통”
test$grp.Peace_1[grp.Peace==3] <- “3_평화 높음”
test$Gender_1[Gender==1] <- “1_남자”
test$Gender_1[Gender==2] <- “2_여자”
detach(test)

# 변수값을 변수값 설명으로 대체한 변수로 교차표 출력
devi02.re <- table(test$grp.Peace_1, test$Gender_1)
devi02.re

# 두 변수의 값에 따른 주변합계를 출력
margin.table(devi02.re)  # grp.Peace_1과 Gender_1 변수의 전체합계
margin.table(devi02.re, 1)  # grp.Peace_1 변수의 주변합계
margin.table(devi02.re, 2)  # grp.Peace_1 변수의 주변합계

# gmodels 패키지를 이용한 교차표 만들기
install.packages(“gmodels”)
library(gmodels)
CrossTable(test$grp.Peace_1, test$Gender_1, digits=2, prop.c=TRUE, prop.r=FALSE, prop.t=FALSE, prop.chisq=FALSE, chisq=TRUE)
# 유의수준 4%로 검정한 결과
```