# 대출자 채무 불이행 여부 예측
## 순위
17등
<img width="631" alt="개인순위" src="https://user-images.githubusercontent.com/82801470/156597681-d6075c26-060c-43ca-9ce3-2144b0b7dcaa.PNG">

## p2p 대부업체의 고객 데이터를 활용한 채무 불이행 여부 예측 과제 수행

처음 데이터를 받았을 때 feature수가 80개가 넘는 것을 보고 너무 많다고 판단하였고 target feature인 depvar 와 다른 feature 들간의 상관관계 분석을 통해서 feature를 줄여보려고 생각하였습니다. 원핫인코딩 된 feature 들의 상관관계가 너무 적어서 다 없애고 xgboost로 평가해보았으나 점수가 오히려 떨어지는 것을 확인하였고 어떻게 처리를 할 까 생각을 하다가 month_since_last_delinq1~12(몇 달 동안 빚을 갚지 못했는지), emp_length1~12(근속연수) 등 같이 값 자체로 의미가 생길 것 같은 feature 들은 다시 값으로 바꾸어 주었습니다. fico_range_low,high 처럼 상관관계가 서로 99퍼가 나오는 것들은 합쳐서 평균을 낸 값으로 줄여주었습니다. 전처리를 한후 f1 score가 오르는 것을 확인하였습니다.

## 모델
Xgboost로 모델 성능이 잘 나오지 않아서 LightGBM으로 바꾸었을 때 F1 score가 오르는 것을 확인하였습니다.  
test data의 파산비율이 train data의 파산 비율과 비슷할 거랑 생각을 가지고 threshold 값을 비슷하게 맞춰준 결과 성능이 많이 올랐습니다.
