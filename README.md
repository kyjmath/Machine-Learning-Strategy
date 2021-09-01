# Machine-Learning-Strategy

1.	데이터 설명
-	stockclose.csv : 1990-12-19 부터 2019-10-16 까지 중국 주식 3660 항목의 매일 종가 데이터
-	sh000001 : 1990-12-19 부터 2019-10-16 까지 沪深300(후선300)의 매일 개장가, 최고가, 최저가, 종가, 거래량 데이터. 1990-12-19의 종가를 100으로 기준


2.	배경
Name of technical indicator:| Type of technical indicator:
------|------
Momentum | Oscillators
Accumulation Distribution Oscillator | Oscillators
Fast Stochastics %K | Stochastics
Median Price | Indicators
Fast Stochastics %D | Stochastics
Negative Volume Index |Indexes
Highest High |Indicators
Positive Volume Index | Indexes
Lowest Low  | Indicators
Slow Stochastics %K | Stochastics
Price and Volume Trend  |Indicators
Slow Stochastics %D  |Stochastics
Accumulation Distribution Line | Oscillators
Acceleration Between Times  | Oscillators
Relative Strength Index  | Indexes
Bollinger Bands | Indicators
Volume Rate of Change | Indicators
PercentB  |Indicators
Price Rate of Change | Indicators
Bandwidth | Indicators
On-Balance Volume | Indicators
Volatility | Stochastics
Chaikin Volatility | Stochastics
William’s % R | Stochastics
William’s Accumulation Distribution Line | Indicators

- 수많은 스토캐스틱 지수를 통해 주가의 상승과 하락을 예측할 수 있다. 머신러닝을 이용해 이 지수들의 예측 성능을 평가하고 최적의 매수, 매도 포지션 포트폴리오를 제작한다.


3.	문제 접근
-	임의의 종목 하나를 골라(000001.SZ) 탐색적 데이터 분석을 한다. 매일 종가 데이터를 통사용해 로그 수익률 계산 후 매주, 매월, 매분기, 매년 수익률 분석을 한다 (수익률 분포 및 샤프비율).
-	이동평균선을 이용하여 매수 매도 신호 칼럼 추가, 실제 신호대로 거래했을 시의 수익률 분석

-	스토캐스틱 지수를 사용하여 (Fast Stochastics, Slow Stochastics, William's R, Ex-post Volatility) 과거 한달의 데이터(20일)를 가지고 다음날의 주가 상승, 하락 수준을 예측하는 칼럼을 추가한다. 

-	실제로 주가가 하락했는지 상승했는지 표시해주는 label칼럼을 추가한 후, decision tree를 이용해 지표의 성능을 평가한다. 또 여러 rolling window와 모델의 파라미터 변경으로 최적의 모델을 찾는다.

-	6개의 지표(Price and Volume Trend, On-Balance Volume, Price Rate of Change, Volume Rate of Change, Accumulation Distribution Line, William’s Accumulation Distribution Line)를 추가한 후 decision tree로 성능을 확인한다.
-	최종적으로 adaboost와 random forest로도 성능을 평가해보고 전략 포트폴리오를 만든다.





4.	결론
-	이동평균선의 매수, 매도 신호를 사용한 전략은 주가가 하락할 때 반응이 신속하지 못해 손실 발생 가능성이 있지만, 상승할 때는 그만큼 초과 수익을 얻기가 쉽다.
연 수익률은 0.71%이 나왔다. 좋은 전략으로 보이지는 않았다.
-	20일의 rolling window를 가진 4개의 지표의 분류 성능은 67%가 나왔다. 상당히 좋은 분류 성능이다.
-	2개월, 1분기, 반년, 1년의 다른 rolling window를 주어서 cross validation 검증을 했을 때 모델의 성능은 80%까지 올라갔고 이때의 rolling window는 2개월(40일)이였고, Decision tree의 최적의 깊이는 4였다.
-	6개의 지표를 추가해 총 10개의 지표로 예측 했을 때는 성능이 75%가 나왔다. 최적의 파라미터 값을 찾아 실행했을 때는 81%가 나왔다.
-	Adaboost와, Random Forest를 사용했을 때는 각각 성능이 83%, 82%가 나왔다. 

