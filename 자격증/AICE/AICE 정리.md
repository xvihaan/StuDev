
# 기초 개념

### .describe()
계산 가능한 값(수치형 변수)에 대한 통계 정보 확인
`df.describe()`

### .isnull()
단순히 `.isnull` 만 사용하기도 하지만 `sum()` 과 함께 사용. 행이나 열별로 Null 개수를 셈
`df.isnull().sum()`

### .value_counts()
범주형 변수에 대해 각 범주별 빈도수 확인
- `normalize = True` 를 주면 정규화된 값으로 범주별 비율 확인
`df[열 이름].value_counts(normalize = False/True`

### .select_dtypes()
원하는 데이터 타입에 해당하는 열만 데이터 프레임 형태로 확인
- `type`: int, float, str, object(O)등의 원하는 데이터 타입의 열만 추출
- `.columns`를 활용해 열 이름만 추출 가능
`df.select_dtypes(type)`

### .replace()
값변경
원하는 값으로 변경하기 위해 사용하며 결측값 대체나 범주형 변수를 라벨링할 때 사용
- `to_replace`: 주로 {'바꾸고자하는 값' : '바뀌는 값'}의 딕셔너리 형태
- `inplace=True` : 변수를 할당하지 않고 바로 적용

`df.replace({'바꾸고자하는 값 : '바뀌는 값'}, inplace=False/True `

### .fillna()
결측값 대체
- `inplace=True` : 변수를 할당하지 않고 바로 적용할 수 있다
`df[열이름].fillna('바뀌는 값', inplace=False/True)`

### .dropna()
결측치 있는 데이터 지우기
`df = df.dropna(subset=['sex_type']`

### .astype()
데이터 프레임 열 타입 변환
`astype`은 바꾸고자 하는 열에 할당해주어야 변환 값이 적용
- type: int, float, str, object 등으로 원하는 타입으로 변환
`df['열이름] = df['열이름'].astype(type)`

### MinMaxScaler (정규화/표준화- 스케일링)
`MinMaxScaler`를 사용하기 위해서는 로드 과정 필요
- fit : 기준이 되는 데이터를 기반으로 스케일러 값 맞춤
- transform : 기준 값을 기반으로 스테일링 적용

```
from sklearn.preprocessing import MinMaxScaler

mms = MinMaxScaler()
X_train = mms.fit_transform(X_train)
X_test = mms.transform(X_test)
```

### LabelEncoder (라벨 인코딩)
LabelEncoer를 사용하기 위해서 로드 과정
- fit : 기준이 되는 데이터를 기반으로 인코더 값 맞춤
- transform : 기준 값을 기반으로 인코딩 적용

```
import sklearn.preprocessing import LabelEncoder

le = LabelEncoder()

df['범주형 열'] = le.fit_transform(df['범주형 열'])
```

### .get_dummies() (원-핫 인코딩)
원-핫 인코딩은 pandas 내 메소드로 적용
- columns : 원-핫 인코딩을 적용할 열 리스트
- drop_first=True : 첫번째 범주는 제외하고 원-핫 인코딩 적용
`df = pd.fet_dummies(data=df, columns=['범주형 열'], drop_first=True)`

### 모델 검증
- 회귀 모델(Regressor): MSE. RMSE, MAE, ...
- 분류 모델(Classifier): Accuracy, Precision, Recall, F1 Score, ...

## 머신러닝 모델링

### LogisticRegression (로지스틱 회귀, 분류)
- C : 규제 강도
- max_iter: 반복횟수

```
from sklearn.lineal_model import LogisticRegression

lg = LogisticRegression(C=1.0, max_iter=1000)

lf.fit(X_trian, y_train)

lf.score(X_test, y_test)
```

### Decision Tree (의사결정 나무, 분류/회귀)
#### DecisionTreeClassifier / DecisionTreeRegressor
- max_depth: 트리 깊이
- random_state: 랜덤 시드

```
from sklearn.tree import DecisionTreeClassifier # 분류
from sklearn.tree import DecisionTreeRegressor # 회귀

dt = DecisionTreeClassifier(max_depth=5, random_state=120)

dt.fit(X_train, y_train)

dt.score(X_test, y_test)
```

### Random Forest (랜덤 포레스트, 분류/회귀)
#### RandomForestClassifier / RandomForestRegressor
- n_estimators: 사용하는 트리 개수
- random_state: 랜덤 시드

```
from sklearn.tree import RandomForestClassifier # 분류
from sklearn.tree import RandomForestRegressor # 회귀

rf = RandomForestClassifier(n_estimators=100, random_state=120)

rf.fit(X_train, y_train)

rf.score(X_test, y_test
```

### XGBoost
#### XGBClassifier / XGBRegressor

### Light GBM
#### LGBClassifier / LGBRegressor


## 딥러닝 모델링

```
example 
# 첫번째 레이어 - unit: 128, activation: relu, input_shape: (26,)
# 두번째 레이어 - unit: 64, activation: relu
# 세번째 레이어 - unit: 32, activation: relu
# 각 히든 레이어 사이에는 0.3비율의 Dropout 적용
# 아웃풋 레이어 - activation: sigmoid
```

```
# import
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Dropout

# 모델 생성
model = Sequential()

# 모델 구조
model.add(Dense(128, input_shape=(26,), activation='relu'))
model.add(Dropout(.3))
model.add(Dense(64, activation='relu'))
model.add(Dropout(.3))
model.add(Dense(32, activation='relu'))
model.add(Dropout(.3))
# output layer의 unit 수는 타겟 변수의 범주 개수와 동일하다.
model.add(Dense(1, activation='sigmoid')) 

# 모델 요약
model.summary()
```

### model.complie
딥러닝은 머신러닝과 달리 모델링 과정에서 컴파일이 필요

```
# 모델 컴파일
model.compile(optimizer='adam',
			  loss='binary_crossentropy', 
              metrics=['accuracy'])
```

### EarlyStopping (callbacks)
모델의 과대적합을 방지하기 위해 학습이 개선되지 않는다면 학습 종료
- monitor: 학습되는지 확인하는 기준
- mode: 모델 최적화의 기준 - 최대화/최소화
- patience: 모델 성능이 개선되지 않을 때 지켜보는 횟수
- verbose: 정보 표시 정도(0,1,2)

```
# import
from tensorflow.keras.callbacks import EarlyStopping

es = EarlyStopping(monitor='val_loss', mode='min', verbose=1)
```

### ModelCheckpoint (callbacks)
모델을 학습하는 과정에서 일정한 간격으로 모델의 가중치를 저장하며 최적 모델을 선택
- filepath: 모델 저장 경로
- monitor: 모니터링하는 지표
- mode: 모델 최적화의 기준 - 최대화/최소화
- verbose: 정보 표시 정도(0,1,2)
- save_best_only=True: 가장 좋은 성능의 모델만 저장

```
# import
from tensorflow.keras.callbacks import ModelCheckpoint

mc = ModelCheckpoint('my_checkpoibnt.ckpt',
					 monitor='val_loss', 
                     mode='min', 
                     save_best_only=True)
```

### fit
- `validation_data`: 검증용 데이터.  
    종속변수와 타겟변수의 쌍으로 입력해야 한다.
- `epochs`: 학습 반복 횟수
- `batch_size`: 학습 시 한 번에 학습하는 데이터 사이즈
- `callbacks`: EarlyStopping, ModelCheckpoint와 같은 학습 과정에서 호출되는 함수

```
history = model.fit(X_train, y_train,
					validation_data = (X_test, y_test),
                    epochs=epochs,
                    batch_size=batch_size,
                    callbacks=[es, mc])
```

### history
```
# 시각화 예시
plt.plot(history.history['loss'], label='Train Loss')
plt.plot(history.history['val_loss'], label='Validation Loss')
plt.xlabel('Epochs') 	# X축 라벨
plt.ylabel('Loss')		# Y축 라벨
plt.legend()			# 범례 표시 - label값
plt.show()
```


# 샘플문항

## 컬럼에 대한 분포도 (countplot, indexing)
* Seabron을 활용하세요
* 첫번째, Adress1(주소1)에 대해서 분포를 보여주는 countplot 그래프를 그리세요
* 두번째, 지역명이 없는 '-' 에 해당되는 row(행)을 삭제하세요
* 출력된 그래프를 보고 해석한 것으로 옳지 않는 선택지를 아래에서 골라 '답안04' 변수에 저장하세요. (예. 답안04=4)
1. Countplot 그래프에서 Address1(주소1) 분포를 확인시 '경기도' 분포가 제일 크다
2. Address1(주소1) 분포를 보면 '인천광역시' 보다 '서울특별시'가 더 크다
3. 지역명이 없는 '-'에 해당되는 row(행)가 2개 있다.

```python
import seaborn as sns

sns.countplot(data=df, x='Address1')

#Boolean indexing
cond = (df['Address1'] == '-')
idx = df[cond].index
df.drop(idx, axis=0, inplace=True)

# df = df[df['Address1]!= '-']
```


## 전처리 수행
- 대상 데이터프레임: df
- jointplot 그래프를 보고 시속 300 이상 되는 이상치를 찾아 해당(row) 삭제
- 불필요한 'RID' 컬럼 삭제
- 전처리 반영 후 새로운 데이터프레임 변수명 df_temp 에 저장

```python
cond = df['Speed_Per_Hour'] >= 300
df[cond]

df.drop([345], axis=0, inplace=True)
df_temp = df.drop('RID', axis=1)

# df_temp = df[df['Speed_Per_Hour'] < 300]
```

## 원핫 인코딩 컬럼데이터 변환
- 대상 df : df_del
- 원핫 인코딩 대상: object 타입의 전체컬럼
- 활용 함수: Pandas의 get_dummies
- 해당 전처리가 반영된 결과를 데이터프레임 변수 df_preset 저장
```python
cols = df_del.select_dtypes('O').columns # 또는 'object'

df_preset = pd.get_dummies(data=df_del, columns=cols)
```

## DecisionTree, RandomForest mae 성능 평가
```python
from sklearn.metrics import mean_absolute_error

y_pred_dt = dt.predict(X_valid)
dt_mae = mean_absolute_error(y_valid, y_pred_dt)

y_pred_rf = rf.predict(X_valid)
rf_mae = mean_absolute_error(y_valid, y_pred_rf)

# 확인
dt_mae
rf_mae

답안12='randomforest'
```


# 딥러닝/머신러닝 코드 정리



## EarlyStopping, ModelCheckPoint

```python
# 딥러닝 필요한 라이브러리 가져오기
# Sequential : 위의 전체 그림 레이아웃이라고 보시면 됩니다.
# Dense : 히든 레이어, 아웃풋 레이어을 가르키는 층으로 보시면 됩니다.
# EarlyStopping : callback으로 매 학습마다 성능을 측정하고 성능이 더 이상 나아지지 않으면 조기종료
# ModelCheckpoint : 주로 성능이 제일 좋을때 모델을 저장하는데 사용

import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.callbacks import EarlyStopping, ModelCheckpoint
```

```python
# 모델 성능이 더이상 좋아지지 않는데, 50번이나 학습하고 있다. 조기 종료와 성능 좋은 모델을 저장
# 모델 학습 : fit() 함수 활용
# 지도학습이므로 데이터와 정답을 주어야 됩니다. : X_train, y_train
# X 데이터를 몇번 공부할지 , 학습할지 횟수를 정합니다. : epochs=50,
# X 데이터를 쪼개서 학습하도록 합니다. : batch_size=8
# X_test, y_test 테스트 데이터셋으로 학습 잘되는지 검증 합니다. : validation_data=(X_test, y_test)
# 학습결과 저장 : history

# EarlyStopping : 매 epoch 마다 'val_loss' 측정해서 3번 동안 더 이상 성능이 나아지지 않으면 조기 종료
es = EarlyStopping(monitor='val_loss', patience=3, verbose=1)

# ModelCheckpoint : 매 epoch 마다 'val_loss' 측정해서 이전보다 성능이 더 좋아지면 모델을 저장
mc = ModelCheckpoint('best_model.h5', monitor='var_loss', save_best_only=True, berbose=1)

history = model.fit(X_train, y_train, epochs=50, batch_size=8, validation_data=(X_test, y_test), callbacks=[es, mc])
```

## 학습된 딥러닝 모델을 가지고 tip 예측
```python

# 0 라인 샘플 데이터을 모델 입력해서 예측하기
# rfr 모델의 predict 함수 활용
# 입력 : X_test[0:2], 결과 : pred 저장
# pred 결과 출력

pred = model.predict(X_test[0:2])
print(pred)
```

