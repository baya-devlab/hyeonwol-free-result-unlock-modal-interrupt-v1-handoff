# 현월 Closeout Evidence Pack

## 1. 결론 요약

* paid ads stopped: 2026-06-28 15:46 KST
* 첫 Meta spend 발생일: 2026-06-06
* 첫 order truth 매출일: 2026-06-02
* 총 광고비: 726,775원
* 총 매출: 436,620원
* gross ROAS: 0.601
* 990원 매출: 215,820원
* 13,800원 매출: 220,800원
* 환불/취소: 환불 0건 / 취소 이벤트 0건 / 실패 이벤트 0건

## 2. 핵심 판단 재료

* paid acquisition 전체 기준 ROAS는 1 미만입니다.
* 990원 상품은 반복 구매를 만들었지만 광고비 회수에는 구조적으로 불리했습니다.
* 13,800원 상품 매출은 발생했지만, 안정적인 업셀 엔진으로 보기에는 증거가 부족합니다.
* 무료 결과/해금 modal/전문 블러 UX는 이벤트 신호를 만들었으나, 최종 매출 효율을 충분히 끌어올리지는 못했습니다.

## 3. 포함 파일

* docs/hyeonwol-financial-summary.md
* docs/meta-hyeonwol-spend-summary.md
* docs/hyeonwol-revenue-summary.md
* docs/hyeonwol-funnel-summary.md
* docs/hyeonwol-product-timeline.md
* docs/hyeonwol-lessons-evidence.md
* data/*.csv
* json/*.json
* raw-links-hyeonwol-closeout.md
* manifest-hyeonwol-closeout.json

## 4. 데이터 신뢰도

* Meta spend: high. Meta Marketing API direct read.
* Revenue: high for aggregate order truth from Admin.
* Refund/cancel: medium. Admin aggregate/payment event status 기반.
* 2026-06-28 cutoff: medium. 종료 시각 15:46 KST 이후 spend가 거의 없다는 전제이나, API는 일별 reporting 제약이 있습니다.
* 광고별 order attribution: medium. order snapshot 영속화 전 구간이 섞여 있습니다.
* Funnel conversion: medium/low for exact purchase conversion. 이벤트/결제 계측 변경 전후가 섞여 있어 방향성 자료로 봐야 합니다.

## 5. 변경하지 않은 것

* Meta write: 수행 안 함
* 광고 ON/OFF: 수행 안 함
* Production deploy: 수행 안 함
* code modification: 수행 안 함
* DB modification: 수행 안 함
* real/test payment: 수행 안 함
