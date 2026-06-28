# 현월 퍼널 요약

## 기준

* 집계 기간: 2026-06-02 ~ 2026-06-28 15:46 KST
* 데이터 소스: Production Admin event aggregate
* 결제 성공은 order truth와 별도로 표시합니다.

## 핵심 이벤트

| event | count | note |
| --- | --- | --- |
| landing_view | 201 |  |
| input_start | 500 |  |
| free_result_view | 441 |  |
| unlock_choice_modal_open | 325 |  |
| unlock_choice_share_select | 105 |  |
| unlock_choice_pay_select | 27 |  |
| unlock_granted | 105 |  |
| speed_dohwa_decode_payment_start | 44 |  |
| speed_dohwa_decode_purchase_success | 218 |  |
| deep_opening_upsell_view | 44 |  |
| deep_opening_payment_start | 3 |  |
| deep_opening_purchase_success | 16 |  |

## 핵심 비율

* free_result_view → any_select: 29.9%
* free_result_view → payment_start event: 10.7%
* 990 purchase truth / free_result_view: 49.4% (주의: order truth와 event denominator가 같은 계측 범위가 아닐 수 있음)
* deep payment_start event → 13,800 purchase truth: 533.3% (주의: 동일 계측 범위 아님)

## 해석 주의

* 2026-06 중간에 무료 결과 UX, unlock modal, Pixel, attribution 보강이 여러 차례 바뀌었습니다.
* event count는 상품 전체 학습에는 유용하지만, 결제 성공률 계산에는 order truth와 직접 나눠 단정하지 않아야 합니다.
* 광고 종료 회고에서는 `free_result_view`, `any_select`, `payment_start event`를 상단/중단 퍼널 신호로 보고, revenue는 order truth를 별도로 보세요.
