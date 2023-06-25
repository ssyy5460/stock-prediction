## 프로젝트 개요

---

- 목적 : 주가 시계열 빅데이터를 사용하여 다음 날 종가의 상승 여부를 예측하고 자동매매 프로그램을 통해 높은 수익률을 산출하는 모델 구현
- 기간 : 2022.01.03~2022.04.01
- 분석도구 : Python


## 1. 배경
- 주가 빅데이터는 수 년 동안 수 천 개 종목의 가격 변화를 기록한 연구적으로 중요한 가치를 가지는 패널 시계열 빅데이터임
- 코로나 이후 나타난 주가의 높은 변동성과 극단적인 수익률로 개인투자자의 과도한 거래를 유발함
- 개인투자자의 저조한 직접투자성과로 전문적 자문서비스의 (AI,ML)활용도를 높이는 방안을 모색할 필요성이 대두됨
- 투자역량이 부족한 개인투자자들의 성과도출에 도움이 되는 자동매매 프로그램을 구축하는 것을 목표로 함

## 2. 문제 정의
<br>
<aside>
💬 전체 약 2000개의 종목 중에서 2018년부터 존속하였던 기업 중 거래대금 * 이상 발생했던 특정 날짜에 대해 <br>
   다음 날 종가가 *% 이상 상승하는지 머신러닝으로 예측한 후 자동매매 프로그램을 통해 높은 수익률을 산출한다.

</aside>


## 3. 분석 프로세스

![프로세스](https://github.com/ssyy5460/stock-prediction/assets/64217874/a883dfe7-db24-4420-8159-4123a9fea900)


### STEP 1. 일별 주가 데이터셋구축
![step1](https://github.com/ssyy5460/stock-prediction/assets/64217874/fdf48ace-05e9-4310-ae25-2dcb642a84dc)
<strong>1-1) 데이터 수집</strong>
- 한국증권거래소에서 제공하는 일 단위 주가데이터
- 전체 약 2000개 종목 중에서 2018년부터 존속하였던 종목 중 거래대금이 * (10억/100억/1000억/1조) 이상 발생했던 날짜의 주가

<strong>1-2) 데이터 정의</strong>
- X(독립변수) : 거래대금 * 이상인 종목과 날짜를 기준일(D-0)로 하여 거래일을 기준으로 하여 기준일 포함 N일간(D-(N-1) ~ D-0)의 주가 데이터(시가, 종가, 저가, 종가) 와 거래대금(volumn * close)
- Y(종속변수) : 다음 날 (D+1) 종가 *% 이상 상승 여부

<strong>1-3) 학습 / 검증 / 시험 데이터 분할 및 데이터 정형화</strong>
- 학습데이터 : 2018년 1월 1일 ~ 2020년 12월 31일
- 검증데이터 : 2021년 1월 1일 ~ 2021년 6월 30일
- 시험데이터 : 2021년 7월 1일 ~ 2021년 12월 31일


### STEP 2. 데이터 탐색
<br>
<strong>2-1) 거래대금별 Next Change 값 분포<br>

![2-1](https://github.com/ssyy5460/stock-prediction/assets/64217874/9be8d163-c2f8-4712-8f9c-c4c0d3ecdf77)

2-2) 거래대금별 라벨 분포<br>

![image](https://github.com/ssyy5460/stock-prediction/assets/64217874/4f803ed4-3399-4cc9-859d-ba30e8736ad9)

2-3) 이상치 탐색<br>

2-4) 이상치 주식 종목 확인<br>
![step 2](https://github.com/ssyy5460/stock-prediction/assets/64217874/b79f3923-f111-4b6d-80a4-27cddd44bf18)


### STEP 3. 데이터 전처리
3-1) 이상치 주식 종목 제거</strong>

### STEP 4. 모델링
##### ** 모델의 매수 타이밍 예측 정확도를 향상시켜 높은 수익률 산출**

1. 다양한 모델 사용
2. 거래대금값을 조정하여 데이터 구축 및 학습 진행
3. 데이터의 종목마다 가격 스케일(천원 대, 만원 대 , 십만원 대 종목)이 다르므로 표준화
4. 다음날 종가의 변화율의 임계값 변화
5. 거래일 변화
6. 성과 지표
- Accuracy / ROC : 다음날 주식 상승 여부를 얼마나 잘 예측하는지?

### STEP 5. 주식 자동매매 프로그램
1. 다음날 종가 상승 여부 예측 확률에 따라 분할매수하여 주문요청일지 작성
2. 자동매매 프로그램을 작성하여 수익률 산출
