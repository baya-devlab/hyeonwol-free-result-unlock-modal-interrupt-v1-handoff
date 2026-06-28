# 현월 매출 요약

## 기준

* 집계 기간: 2026-06-02 ~ 2026-06-28 15:46 KST
* 데이터 소스: Production Admin API, orders.status=PAID aggregate
* 공개 산출물에는 주문자/결제 원문을 포함하지 않았습니다.

## 총합

* gross revenue: 436,620원
* net revenue: 436,620원
* paid order count: 234
* failed payment events: 0
* cancelled payment events: 0
* refunded rows: 0
* refund amount: 0원

## 상품별

| product | paid count | gross revenue | unit price |
| --- | --- | --- | --- |
| 990원 속도화 해독 | 218 | 215,820원 | 990원 |
| 13,800원 심층 개안 | 16 | 220,800원 | 13,800원 |

## 주의

* 결제 성공 truth는 order row 기준입니다.
* 일부 브라우저 이벤트는 배포/계측 변경 전후로 누락될 수 있어, order truth와 이벤트 count가 단조 증가하지 않습니다.
* 그래서 회고의 최종 매출은 order truth를 우선하고, 퍼널 전환율은 별도 보조 지표로만 사용합니다.
