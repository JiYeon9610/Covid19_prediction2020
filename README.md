# 2020 경기도 데이터 기반 코로나19 예측 공모전
2020.09.25 제출

목적: 9/30 ~ 10/4 연휴 기간의 경기도 코로나 확진자 수 예측 모델



## 1. 활용 데이터 설명
9월 23일까지의 일일 데이터를 활용하여 9/30~10/4까지의 확진자 수 예측
Y 레이블: 경기도 일일 확진자수



### 1. 코로나의 직접적인 요인
코로나 관련 주요 이슈들, 정부 정책 단위의 통제, 시민들의 경각심이 확진자 추이에 직접적인 영향을 미쳤을 것이라 판단.
이에 따라 관련 정보를 대변할 수 있는 데이터를 수집한 후, 시각화 진행.

1-1. 가설: 코로나 확산 방지 대책과 관련한 정부의 정책이 확진자 추이에 선행하여 유의미한 영향을 미칠 것이다.
데이터: 정부 정책 관련 뉴스 기사의 개수 데이터 크롤링
-코로나_단계 : 코로나에 대응하여 정부가 선언하는 거리두기 단계의 변동 관련 데이터 수집 ("코로나+단계"를 제목에 포함하고 잇는 일별 뉴스 개수 수집)
-마스크_의무화 : 코로나에 대응하여 정부가 선언하는 마스크 의무화 정책 시행 데이터 수집("마스크+의무화"를 제목에 포함하고 있는 일별 뉴스 개수 수집)
-코로나_고위험_시설 : 코로나 전파 위험성이 높은 고위험 시설에 대한 이슈, 이와 관련된 정부의 제재 정책 시행 데이터 수집("코로나+고위험+시설"을 내용에 포함하고 있는 일별 뉴스 개수 수집)
-> Data_collection_preprocessing.ipynb

1-2. 가설: 시민들의 경각심(사회적 거리두기) / 코로나 쥬요 이슈(집단 감염,발병)가 확진자 추이에 선행하여 유의미한 영향을 미칠 것이다.
데이터: 코로나 관련 키워드의 네이버 검색어 추이 데이터 수집
-사회적_거리두기: 코로나 관련하여 시민들의 경각심 정도를 측정하기 위한 지표 데이터 수집('사회적 거리두기', '거리두기', '사회적 거리' 키워드)
-집단_감염: 코로나 확산의 주요 원인이자 이슈가 되는 집단 감염 사태의 심각성을 측정하기 위한 지표 데이터 수집('집단 감염', '집단 발병' 키워드)
-> https://datalab.naver.com/


### 2. 코로나의 외부적인 요인
사람들이 이동하는 것이 코로나 확산의 주요 원인 중 하나라고 판단.
이에 따라 코로나에 직접적인 영향을 행사하지는 않더라도, 인구의 이동에 영향을 미쳤을 법한 외부적인 요인도 확진자 추이에 영향을 미쳤을 것이라고 판단하여 관련 데이터 수집한 후, 시각화 진행.

2-1. 가설: 날씨의 컨디션이 사람들의 이동에 영향을 미쳤을 것이다.
기상청 기상자료개방포털 데이터 활용(https://data.kma.go.kr). 
경기도에 해당하는 지역의 지표들의 평균값 도출.
'평균기온' 변수값과 '평균 상대습도' 변수 값을 불쾌지수 공식에 대입하여 값 산출.

2-2. 가설: 주말 및 공휴일 여부가 사람들의 이동에 영향을 미칠 것이다.
주말을 포함한 공휴일 데이터 작성.
