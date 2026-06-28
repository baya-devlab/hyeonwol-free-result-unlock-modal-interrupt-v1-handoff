# 현월 Paid Acquisition 종료 회고

## 2026-06-02 ~ 2026-06-28

## 1. 한 줄 결론

현월은 **무반응 상품은 아니었다.**

990원 구매 218건, 13,800원 구매 16건, 총 매출 436,620원을 만들었다. 그러나 총 광고비 726,775원 대비 gross ROAS는 0.601에 그쳤고, paid acquisition만으로 광고비를 회수하는 구조는 성립하지 않았다. 따라서 2026-06-28 15:46 KST 기준으로 현월의 유료 광고 집행은 중단하고, 상품과 퍼널에서 얻은 자산은 다른 연애/재회/결혼 사주 상품에 재활용한다.

---

## 2. 종료 결정

### 결정

```text
2026-06-28 15:46 KST 기준,
현월 상품의 paid acquisition을 중단한다.
```

### 의미

현월 상품을 완전히 삭제하거나 부정하는 것이 아니라, 유료 광고 주력 상품으로서의 운영을 중단한다는 뜻이다.

현월은 다음과 같은 자산으로 보관한다.

* 도화/겉도화/속도화 IP
* 다크로맨스 사주 브랜드 톤
* 무료 결과 -> 선택형 해금 modal -> 블러 전문 섹션 구조
* 사주원국 기반 개인화 카피
* Meta 표준 이벤트 + Admin order truth reconciliation 운영 경험
* Core 소재 / 신규 소재 screening 분리 구조

---

## 3. 정산 기준

| 항목 | 기준 |
| --- | --- |
| paid ads 종료 시점 | 2026-06-28 15:46 KST |
| 첫 Meta spend 발생일 | 2026-06-06 |
| 첫 order truth 매출일 | 2026-06-02 |
| 광고비 기준 | Meta direct spend |
| 매출 기준 | Admin order truth |
| 데이터 신뢰도 | Meta spend high, revenue high, 광고별 attribution medium |

Codex closeout evidence pack 기준, Meta spend는 Meta Marketing API direct read로 high confidence이고, revenue는 Admin aggregate order truth 기준 high confidence다. 다만 2026-06-28 15:46 KST cutoff는 Meta API의 일별 reporting 제약 때문에 medium confidence이며, 광고별 order attribution도 snapshot 영속화 전 구간이 섞여 medium confidence다.

---

## 4. 총 지출 / 총 매출 / ROAS

| 지표 | 값 |
| --- | ---: |
| 총 광고비 | 726,775원 |
| 총 매출 | 436,620원 |
| gross ROAS | 0.601 |
| net ROAS | 0.601 |
| 광고비 대비 손익 | -290,155원 |
| 990원 매출 | 215,820원 |
| 13,800원 매출 | 220,800원 |
| 990원 구매 | 218건 |
| 13,800원 구매 | 16건 |
| 전체 구매당 광고비 | 3,106원 |
| 990원 CPA | 3,334원 |
| 13,800원 CPA | 45,423원 |
| payment_start event당 광고비 | 15,463원 |
| free_result_view당 광고비 | 1,648원 |
| any_select당 광고비 | 5,506원 |

총 광고비는 726,775원, 총 매출은 436,620원, gross ROAS는 0.601로 paid acquisition만으로 광고비를 회수하지 못했다. 990원 상품은 구매를 만들 수 있었지만 단가가 낮아 광고비 회수 구조가 약했고, 13,800원 상품은 전체 매출의 상당 부분을 만들었지만 deep 구매당 광고비가 높았다.

---

## 5. 성과 해석

### 5.1 현월은 완전 무반응 상품이 아니었다

현월은 실제 구매를 만들었다.

* 990원 구매: 218건
* 13,800원 구매: 16건
* 총 매출: 436,620원

따라서 “아무도 사지 않은 상품”은 아니었다.

하지만 paid acquisition에서 중요한 것은 구매 발생 여부가 아니라, 광고비를 감당할 만큼의 객단가와 전환율이 안정적으로 나오는가다. 이 기준에서는 현월은 실패했다.

### 5.2 990원 상품은 구매를 만들었지만 광고비 회수에는 불리했다

990원 상품은 218건의 구매를 만들었다. 하지만 990원이라는 가격대는 paid traffic에서 단독 수익원이 되기 어렵다.

* 990원 매출: 215,820원
* 990원 CPA: 3,334원

990원 상품 하나를 팔기 위해 평균 3,334원의 광고비가 들어간 구조다. 즉, 990원 front-end는 진입 장벽을 낮추는 역할은 했지만, 수익성을 책임질 수는 없었다.

### 5.3 13,800원 업셀은 “발생은 했지만 안정적 엔진은 아니었다”

전체 누적 기준으로 13,800원 구매는 16건 있었다. 즉, 13,800원 상품이 전혀 팔리지 않은 것은 아니다.

하지만 13,800원 CPA는 45,423원으로 높았고, 전체 ROAS를 1 이상으로 끌어올릴 만큼 안정적이지 않았다.

따라서 최종 병목은 이렇게 정리하는 것이 정확하다.

```text
13,800원 업셀이 전혀 없었던 것이 아니라,
광고비를 회수할 만큼 안정적인 upsell engine으로 작동하지 못했다.
```

### 5.4 마지막 Pixel-fix 이후 구간은 더 나빴다

다른 스레드 분석 기준, 마지막 Pixel-fix 이후 소액 재개 구간에서는 다음과 같은 수치가 보고됐다.

* spend: 46,459원
* revenue: 11,880원
* ROAS: 0.256
* 13,800원 구매: 0건

이 수치는 전체 누적과 별개로, 계측이 복구된 뒤 최신 퍼널/광고 조건에서도 ROAS가 회복되지 않았다는 보조 근거다.

따라서 최종 판단은 다음과 같다.

```text
전체 누적으로도 ROAS 0.601로 부족했고,
마지막 정상 계측 구간에서도 개선 신호가 충분하지 않았다.
```

---

## 6. 주요 타임라인

### 2026-06-02 ~ 2026-06-06: 상품/매출/광고 시작

* 첫 order truth 매출일: 2026-06-02
* 첫 Meta spend 발생일: 2026-06-06

### 2026-06 중순: 무료 결과 -> 해금 퍼널 고도화

핵심 문제는 무료 결과페이지 도달 대비 전문 열람 행동이 낮다는 점이었다.

이를 해결하기 위해 다음 구조가 도입됐다.

```text
무료 결과페이지
-> 겉도화 개요
-> 겉도화 카드
-> 왜 이렇게 나왔는가
-> 겉도화 해석 + partial blur
-> 도화 지표 전문 블러
-> {personaName}의 진모습 블러
-> 원국 해석 전문 블러
-> LOCKED · 전문 최종 CTA
```

핵심 UX 변경:

* 초반 반복 블러 피로감 축소
* 무료 결과 전반부의 “내 얘기 같다” 강화
* 사주원국 기반 근거 제시
* 도화 지표에서 자동 모달 1회 노출
* partial blur + 전문 보기 CTA
* 공유 / 990원 선택형 unlock modal

### 2026-06-25 전후: 소액 광고 재개

무료 결과페이지 개편 후, Production UX와 이벤트 row가 광고 소액 재개 가능한 수준으로 확인되어 광고를 재개했다.

초기 구조:

```text
총 예산: 30,000원/day
Core: HW_990_CORE_SOFT
New screening: HW_NEW_CREATIVE_SCREENING_ABO_20260621
```

### 2026-06-26: Meta Pixel mismatch 발견

Day 1 분석에서 Admin 이벤트와 주문은 살아 있었지만, Meta Ads Insights에서 ViewContent / InitiateCheckout / Purchase 표준 이벤트가 0으로 잡히는 문제가 발견됐다.

원인:

```text
광고세트는 현월 Pixel/Dataset 기준으로 최적화 중
Production /api/payment/config는 공용 DASI pixel을 반환
결과적으로 현월 Pixel에는 표준 이벤트가 들어오지 않음
```

이 문제는 CRITICAL로 판단됐고, 광고를 PAUSE한 뒤 Pixel mismatch fix와 beacon fix가 진행됐다.

### 2026-06-26~27: Pixel / beacon fix

두 단계의 계측 수정이 있었다.

1. Production config가 현월 Pixel을 반환하도록 수정
2. browser runtime에서 facebook.com/tr beacon이 실제 발화되도록 수정

이후 Meta Events Manager UI에서 PageView / ViewContent 수신이 확인됐다.

### 2026-06-26 23:56 KST 이후: Pixel-fix 후 재개

Pixel fix 이후 2차 소액 재개를 진행했다.

최종 재개 구조:

```text
총 예산: 20,000원/day
Core: 10,000원/day
- AD_Share_GeotSok_B_01
- AD_Free_SajuWritten_01

New screening:
- AD_2ND_DangerDohwa_01 5,000원/day
- AD_2ND_SelfOthersGap_01 5,000원/day
```

### 2026-06-27: 예산 mismatch 수정

Core adset 예산이 의도한 10,000원/day가 아니라 15,000원/day로 설정되어 있어, 총 예산이 25,000원/day로 돌아가던 구간이 있었다. 2026-06-27 12:58 KST에 20,000원/day 구조로 복구됐다.

성과 분석에서는 아래처럼 구간을 나눠야 한다.

* A구간: Pixel-fix 후 예산 mismatch 구간
* B구간: Pixel-fix 후 정상 예산 구간

### 2026-06-28 15:46 KST: paid acquisition 중단

최종적으로 2026-06-28 15:46 KST 기준으로 현월 관련 Meta 광고를 모두 OFF하고, 현월 상품의 paid acquisition을 중단했다.

---

## 7. 광고 소재별 학습

### AD_Share_GeotSok_B_01

가장 강한 소재로 남았다.

다른 스레드 분석 기준:

* spend: 21,578원
* revenue: 8,910원
* ROAS: 0.413
* 990 PAID: 9건

판단:

```text
상대적으로 가장 나았지만, 절대 수익성은 부족.
승자 광고라기보다 “가장 덜 나쁜 진단용 소재”.
```

### AD_2ND_DangerDohwa_01

* 일부 하단 기여 신호가 있었다.
* 하지만 단독 scale 후보로 보기에는 ROAS가 낮았다.

### AD_2ND_SelfOthersGap_01

* 클릭/LPV/free_result 측면에서는 반응 가능성이 있었다.
* 일부 990원 구매가 있었으나 수익성은 부족했다.

### AD_Free_SajuWritten_01

* 후보로 포함됐으나, Pixel-fix 이후 active 상태임에도 spend 0이어서 검증이 충분하지 않았다.

### AD_Share_GeotSok_A_01 / AD_2ND_FirstImpression_01 / AD_Free_RedRose_01

* 일부 반응 가능성은 있었지만, 최종 20,000원/day 예산 구조에서는 제외하는 것이 합리적이었다.
* 작은 예산에서는 광고 수를 줄여야 하며, 7개 이상을 동시에 켜는 것은 표본 분산이 너무 컸다.

---

## 8. 실패한 가설

### 8.1 무료 결과 UX를 깊게 만들면 구매가 충분히 증가할 것이다

부분적으로만 맞았다.

무료 결과/해금 modal/전문 블러 UX는 이벤트 신호를 만들었다. 그러나 최종 매출 효율을 충분히 끌어올리지는 못했다.

정리:

```text
UX 개선 -> 열람 의향 이벤트 개선
UX 개선 -> 광고비 회수 가능한 매출 개선
```

첫 번째는 어느 정도 맞았지만, 두 번째는 실패했다.

### 8.2 modal_open 상승은 전환 개선을 의미한다

실패한 해석이다.

자동 모달을 도입하면 modal_open은 쉽게 오른다. 따라서 modal_open은 더 이상 핵심 성공 지표가 아니다.

진짜 지표는 아래다.

* free_result_view -> any_select
* free_result_view -> unlock_granted
* free_result_view -> payment_start
* payment_start -> purchase_success
* 990 purchase -> 13,800 purchase

### 8.3 Pixel 문제만 해결하면 ROAS가 회복될 것이다

실패했다.

Pixel/Dataset mismatch와 track beacon 문제는 실제로 심각했다. 그러나 계측 복구 이후에도 ROAS는 회복되지 않았다.

정리:

```text
계측 문제는 성과 판단을 왜곡한다.
하지만 계측 복구가 상품 economics를 해결하지는 않는다.
```

### 8.4 990원 front-end 상품이 CAC를 완충해줄 것이다

실패했다.

990원 구매는 반복적으로 발생했지만, 가격대가 너무 낮아 광고비 회수에는 구조적으로 불리했다.

### 8.5 신규 소재 screening만으로 ROAS를 반전시킬 수 있다

입증되지 않았다.

여러 소재가 클릭과 일부 구매를 만들었지만, ROAS를 구조적으로 뒤집을 만큼 강한 winner는 나오지 않았다.

---

## 9. 유효했던 가설

### 9.1 무료 결과의 근거 제시는 열람 의향을 높인다

사주/운세류 상품에서는 단순 결과보다 “왜 이렇게 나왔는가”가 중요하다.

재활용 가능한 요소:

* 원국표
* 월지/일지/일간 근거 설명
* 쉬운 오행 표기
* 유형별 개인화 근거 문장
* partial blur
* 전문 결과 일부 예고

### 9.2 선택형 unlock modal은 강제 공유 병목을 완화한다

공유만 강제하는 구조보다, 아래 두 선택지를 제시하는 구조가 더 낫다.

```text
A. 카카오톡 공유하고 무료 열기
B. 공유 없이 990원으로 바로 열기
```

이 구조는 다른 상품에도 재활용할 가치가 있다.

### 9.3 Pixel / Dataset QA는 광고 재개 전 필수다

이번 현월 실험에서 가장 비싼 시행착오 중 하나는 계측 mismatch였다.

향후 모든 상품에서 광고 ON 전 반드시 확인해야 할 것:

* production config pixel ID
* browser runtime fbq init
* facebook.com/tr beacon
* Events Manager UI 수신
* Ads Insights action 수신
* Admin order truth와 Meta action 비교

### 9.4 Core / Screening 분리 운영은 유효하다

Core 소재와 신규 소재를 분리해 screening하는 운영 구조는 다음 상품에도 재활용 가능하다.

---

## 10. 다른 상품에 재활용할 자산

### 10.1 UX 구조

```text
무료 결과
-> 선택형 해금 modal
-> 블러 전문 섹션
-> 최종 CTA
```

이 구조는 다른 사주 상품에도 유효하다.

특히:

* 재회 사주
* 결혼 사주
* 연애 상대 분석
* 속마음/관계 패턴 분석

에 이식 가능하다.

### 10.2 카피 자산

재활용 가능한 카피 축:

* 첫인상
* 잔상
* 오해
* 사람들이 처음 보는 나
* 상대 기억에 남는 방식
* 관계 안에서 드러나는 태도
* 사주원국이 한쪽을 가리킨다

### 10.3 계측/분석 자산

* Meta 표준 이벤트와 Admin order truth를 함께 보는 방식
* Pixel/Dataset QA 체크리스트
* 구간별 cohort 분리
* spend/revenue/ROAS와 이벤트 퍼널을 같이 보는 방식

### 10.4 운영 자산

* Core campaign / screening campaign 분리
* 작은 예산에서는 소재 수를 줄이는 원칙
* 광고 재개 전 source-of-truth 정리
* public raw handoff 기반 협업 방식

---

## 11. 폐기 또는 보류할 것

### 폐기

* 현월 paid acquisition 풀예산 재개
* 현월 신규 광고 대량 제작
* 현월 무료 결과페이지 추가 대수술
* 990원 단독 수익성 기대

### 보류

* 13,800원 심층 개안 upsell 재설계
* 현월 캐릭터/IP 확장
* 리타겟팅 기반 재활성화
* 유기 유입용 콘텐츠화

---

## 12. 현월을 다시 재개하려면 필요한 조건

현월을 다시 paid acquisition 상품으로 재개하려면 아래 조건이 필요하다.

1. 13,800원 업셀 UX/카피/상품 가치 제안 재설계
2. 990원 구매 후 업셀 전환율을 유기/리타겟팅으로 먼저 검증
3. blended AOV 기준 CPA 허용선 재계산
4. Meta Pixel/standard event QA 체크리스트 통과
5. 광고 수 3개 이하로 제한한 소액 재개
6. 24시간 단위 cohort 분석
7. 13,800원 구매가 안정적으로 발생하는지 확인

최소 재개 기준은 다음이다.

```text
990원 구매만 발생 -> 재개 불가
13,800원 구매 일부 발생 -> 관찰 가능
blended ROAS 1 근접 또는 초과 -> 재개 검토
```

---

## 13. 최종 판단

현월은 실패한 아이디어가 아니라, paid acquisition 주력 상품으로는 economics가 맞지 않았던 실험이다.

구매와 행동 신호는 있었다.

* 990원 구매: 218건
* 13,800원 구매: 16건
* 총 매출: 436,620원

하지만 광고비 회수에는 실패했다.

* 총 광고비: 726,775원
* gross ROAS: 0.601
* 광고비 대비 손익: -290,155원

따라서 현월은 유료 광고 집행을 중단한다.

다만 현월에서 얻은 아래 자산은 다음 상품에 이식한다.

* 도화/첫인상/관계 해석형 카피
* 무료 결과 -> 해금 modal -> 블러 전문 UX
* 사주 원국 근거 제시 방식
* Meta Pixel QA 체크리스트
* Core/screening 광고 운영 구조
* paid acquisition 회고 체계

### 최종 한 줄 회고

현월은 고객의 호기심과 일부 구매를 만들었지만, 990원 front-end와 불안정한 13,800원 upsell만으로는 paid acquisition 경제성이 성립하지 않았다. 2026-06-28 15:46 KST 기준 유료 광고는 중단하고, 실험에서 얻은 UX·카피·계측·운영 자산은 다음 사주 상품에 이식한다.

---

## 부록: 근거 자료

* Closeout evidence pack: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/closeout/hyeonwol-closeout-20260628-1546/docs/hyeonwol-closeout-evidence-pack.md
* Financial summary: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/closeout/hyeonwol-closeout-20260628-1546/docs/hyeonwol-financial-summary.md
* Meta spend summary: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/closeout/hyeonwol-closeout-20260628-1546/docs/meta-hyeonwol-spend-summary.md
* Revenue summary: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/closeout/hyeonwol-closeout-20260628-1546/docs/hyeonwol-revenue-summary.md
* Funnel summary: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/closeout/hyeonwol-closeout-20260628-1546/docs/hyeonwol-funnel-summary.md
* Product timeline: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/closeout/hyeonwol-closeout-20260628-1546/docs/hyeonwol-product-timeline.md
* Lessons evidence: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/closeout/hyeonwol-closeout-20260628-1546/docs/hyeonwol-lessons-evidence.md
