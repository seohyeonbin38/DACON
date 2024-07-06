# **KPI 도출 비즈니스 전략 아이디어 경진대회**

## Host
- 주최 : Dacon
- 주관 : Dacon
- 기간 : 2024년 4월 8일 10:00 ~ 5월 6일 10:00
- https://dacon.io/competitions/official/236248/overview/description
---
## 🧐 About
데이터를 분석하여 핵심 성과 지표(KPI : ex. MAU, CLV 등)를 도출 및 비즈니스를 위한 전략 방안 제시

### 선정된 핵심 KPI ###
1. 지역별 배송 지연율: 고객 만족도 분석을 기반으로 한 지역 별 배송 지연율
2. 핵심 그룹의 매출 비율: RFM 분석을 통한 핵심 그룹의 매출 비율
3. 시간대별 카테고리 AOV: AOV 분석을 통한 시간대 별 카테고리 AOV  

---
## 📖 Dataset
**Data Source**  [Dateset](https://dacon.io/competitions/official/236248/data)
```
Dataset Info.

customers.csv
- Customer_id : 고객 ID
- Customer_unique_id : 고객 고유 ID
- Customer_zipcode_prefix : 고객 우편번호 앞부분
- Customer_city : 고객 도시
- Customer_state : 고객 주

locations.csv
- Geolocation_zipcode_prefix : 우편번호 앞부분
- Geolocation_lat : 위도
- Geolocation_lng : 경도
- Geolocation_city : 도시(city)
- Geolocation_state : 주(state)

order_items.csv
- Order_id : 주문 고유 ID
- Order_item_id : 동일한 주문에 포함된 품목 수를 식별하는 일련 번호
- Product_id : 제품 고유 ID
- Seller_id : 판매자 고유 ID
- Price : 판매 가격
- Freight_value : 품목 화물 가격

orders.csv
- Order_id : 주문 고유 ID
- Customer_id : 고객 ID
- Order_status : 주문 상태
- Order_purchase_timestamp : 구매 시간
- Order_delivered_carrier_date : 물류 처리 시간
- Order_delivered_customer_date : 실제 배송 날짜
- Order_estimated_delivery_date : 기대 배송 날짜

payments.csv
- Order_id : 주문 고유 ID
- Payment_sequential : 결제 시퀀스(둘 이상의 결제 방법으로 결제 가능)
- Payment_type : 지불 방법 
- Payment_installments : 할부 횟수
- Payment_value : 거래 가치

products.csv
- Product_id : 제품 고유 ID
- Product_category_name : 카테고리 이름
- Product_weight_g : 제품 무게(g)
- Product_length_cm : 제품 길이(cm)
- Product_height_cm : 제품 높이(cm)
- Product_width_cm : 제품 너비(cm)

reviews.csv
- Review_id : 리뷰 고유 ID
- Order_id : 주문 고유 ID
- Review_score : 리뷰 점수
- Review_creation_date : 리뷰 생성 시간
- Review_answer_timestamp : 리뷰 답변 시간

sellers.csv
Seller_id : 판매자 고유 ID
Seller_zipcode_prefix : 판매자 우편번호 앞자리
Seller_city : 판매자 도시(city)
Seller_state : 판매자 주(state)
```

## 🔧 Data Preprocessing
```
1. 지역별 배송 지연율
  - ‘리뷰 기간’, ‘답변 기간’, ‘제품 준비 기간’, ‘실제 배송 기간’, ‘예상 배송 기간’, ‘실제 수령 총기간’, ‘예상 수령 총기간’, ‘수령 차이’ 변수를 추가
  - ○○ 기간 등의 변수들은 날짜 간의 차이를 계산하여 추가
  - 각 기간을 초 단위로 변환한 후 3600(초/시간)과 24(시간/일)을 곱한 값으로 나누어 일 단위로 변경
  - ‘예상 배송 기간’이 음수인 경우는 물류 처리 날짜가 기대 배송 날짜보다 늦은 경우로, 이후 배송 지연율을
    계산하기에 부적합하므로 제거

2. 핵심 그룹의 매출 비율
  - 고객 식별 -> 고객 고유 ID
  - 최근 구매 일자 ->  구매 날짜
  - 구매 빈도 -> 주문 ID
  - 구매 금액 -> 거래 가치

3. 시간대별 카테고리 AOV
  - AOV = 총거래 가치 / 총판매량
  - 시간대별 AOV : 시간대별로 거래 가치의 합과 판매량의 합을 구하여 AOV 계산
  - 시간대별 카테고리 AOV : 각 시간대의 카테고리별 거래 가치의 합과 판매량의 합을 구하여 AOV 계산
  - 시간대별 카테고리 & 지역 AOV : 시간대별로 각 카테고리의 지역별 거래 가치의 합과 판매량의 합을 구하여 AOV 계산
  - 시간대별 카테고리 & 지역 & 주 AOV : 시간대별로 카테고리, 지역, 주의 거래 가치의 합과 판매량의 합을 구하여 AOV 계산
  - 시간대별 카테고리의 고객 등급 : 고객 등급별로 각 시간대의 카테고리를 구매한 고객의 수 계산
```

##  ✍️ Authors
- ``허승빈`` 
- ``서현빈`` 
- ``안성익`` 
- ``임한나`` 
- ``류준호``

---

## 😃 Result
- **Public score** 2nd 9.1 | **Awards** 1st 8.3
- https://dacon.io/competitions/official/236248/codeshare/10409

## 📖 Reference
RFM

[논문: 김동석, 2021](https://oak.jejunu.ac.kr/bitstream/2020.oak/23663/2/RFM%20%EB%AA%A8%ED%98%95%EC%9D%98%20%EA%B0%80%EC%A4%91%EC%B9%98%20%EC%84%A0%ED%83%9D%EC%97%90%20%EA%B4%80%ED%95%9C%20%EC%97%B0%EA%B5%AC.pdf)

[고객 세그먼트](https://documentation.bloomreach.com/engagement/docs/rfm-segmentation)
