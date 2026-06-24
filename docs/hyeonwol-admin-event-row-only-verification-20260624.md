# 현월 Admin Event Row-only Verification 및 광고 재개 판정

## 1. 결론 요약

- 판정: **GO**
- 이유: Admin row-level에서 `free_result_view`, `unlock_choice_modal_open`, `unlock_choice_share_select`, `unlock_granted`, `speed_dohwa_decode_payment_start`가 확인됐다. `unlock_choice_pay_select`는 아직 0이지만, 선택 이벤트는 share route로 확인됐고 payment_start도 row로 확인됐다.
- 광고 재개 범위: 그래도 풀예산보다 **소액/부분 재개부터** 권장한다. 이유는 오늘 표본이 작고 pay-direct 선택은 아직 관찰되지 않았기 때문이다.
- Production URL: https://hyeonwol.dasi.ing/
- Production deployment: `dpl_8FgERhSxNt2uBe4JWnbosKwZ7uos`
- Rollback target: `dpl_55zDkYJkCvZQCTM2zPE2Qv2zzWkv`

## 2. Admin Row-level 이벤트 확인

| event_name | observed | latest_timestamp_kst | today_count | since_deploy_recent_window | recent_1h_recent_window | confidence | notes |
| --- | --- | --- | ---: | ---: | ---: | --- | --- |
| `free_result_view` | yes | 2026-06-24 15:59:27 KST | 2 | 2 | 0 | high | row-level event_name confirmed |
| `unlock_choice_modal_open` | yes | 2026-06-24 15:58:23 KST | 1 | 1 | 0 | high | row-level event_name confirmed |
| `unlock_choice_pay_select` | no | - | 0 | 0 | 0 | high | no row observed in admin range |
| `unlock_choice_share_select` | yes | 2026-06-24 15:58:31 KST | 1 | 1 | 0 | high | row-level event_name confirmed |
| `unlock_granted` | yes | 2026-06-24 15:58:35 KST | 1 | 1 | 0 | high | row-level event_name confirmed |
| `speed_dohwa_decode_payment_start` | yes | 2026-06-24 15:59:01 KST | 1 | 1 | 0 | high | row-level event_name confirmed |
| `speed_dohwa_decode_purchase_success` | no | - | 0 | 0 | 0 | high | no row observed in admin range |

추가 이벤트:

| event_name | observed | today_count | notes |
| --- | --- | ---: | --- |
| `deep_opening_upsell_view` | no | 0 | no row observed in admin range |
| `deep_opening_payment_start` | no | 0 | no row observed in admin range |
| `deep_opening_purchase_success` | no | 0 | no row observed in admin range |

## 3. 핵심 퍼널 집계

기준: Admin 오늘 범위 + 최근 event row window. 오늘은 current-day partial이다.

| step | count | rate_from_previous | rate_from_free_result |
| --- | ---: | ---: | ---: |
| `free_result_view` | 2 | - | 100.0% |
| `unlock_choice_modal_open` | 1 | 50.0% | 50.0% |
| `unlock_choice_share_select` | 1 | 100.0% | 50.0% |
| `unlock_choice_pay_select` | 0 | 0.0% | 0.0% |
| `any_select` | 1 | - | 50.0% |
| `unlock_granted` | 1 | 100.0% | 50.0% |
| `speed_dohwa_decode_payment_start` | 1 | 100.0% | 50.0% |
| `speed_dohwa_decode_purchase_success` | 0 | 0.0% | 0.0% |

핵심 판단 지표:

- `free_result_view -> any_select`: 1/2 (50.0%)
- `free_result_view -> unlock_granted`: 1/2 (50.0%)
- `free_result_view -> speed_dohwa_decode_payment_start`: 1/2 (50.0%)
- `unlock_choice_modal_open -> share_select`: 1/1 (100.0%)
- `unlock_choice_modal_open -> pay_select`: 0/1 (0.0%)

QA 포함 여부: recent event window 기준 QA flag는 핵심 row에서 false였다. 다만 표본이 매우 작으므로 광고 재개 후 실제 paid traffic 기준으로 다시 확인해야 한다.

## 4. GO/NO-GO 재판정

판정: **GO**

근거:

- `free_result_view` row 확인
- `unlock_choice_modal_open` row 확인
- `unlock_choice_share_select` row 확인
- `unlock_granted` row 확인
- `speed_dohwa_decode_payment_start` row 확인
- Production UX와 rollback 기준은 직전 검증에서 확인
- source-of-truth는 draft PR까지 정리됨

보수적 단서:

- `unlock_choice_pay_select`는 아직 row가 없다. pay-direct 분기는 광고 재개 후 추가 확인 필요.
- 오늘 표본은 작다. 따라서 GO는 "광고 재개 가능"이지 "풀예산 확장"이 아니다.

## 5. 광고 재개 권장안

재개 가능 범위:

- 기존 캠페인 일부만 소액 재개.
- 신규 campaign/ad 생성은 불필요.
- 풀예산 재개는 첫 24~48h row 확인 후 판단.

권장 시작 방식:

1. 기존 성과가 있던 Core 일부와 screening 일부만 켠다.
2. 총액은 기존 계획 대비 25~40% 수준에서 시작한다.
3. 첫 24시간은 ROAS보다 event receipt와 중간 퍼널을 본다.
4. Day 2에 `any_select`, `unlock_granted`, `payment_start`, paid order를 재확인한다.

중단 기준:

- `free_result_view`가 광고 유입 대비 현저히 낮음
- `unlock_choice_modal_open`은 있는데 select가 거의 없음
- `speed_dohwa_decode_payment_start`가 계속 0
- Production endpoint 4xx/5xx 발생

증액 기준:

- `free_result_view -> any_select`가 의미 있게 발생
- `unlock_granted`와 `speed_dohwa_decode_payment_start`가 유지
- 990원 paid order 발생
- CPC/CTR과 UX 퍼널이 동시에 유지

## 6. 금지 작업 수행 여부

| 항목 | 수행 여부 |
| --- | --- |
| Production redeploy | no |
| real payment | no |
| test payment | no |
| Meta write | no |
| ad ON/OFF | no |
| budget change | no |
| DB schema change | no |
| env change | no |
| source repo commit/push | no |

## 7. 남은 리스크

- pay-direct 선택 row는 아직 없다.
- 오늘 표본이 작아 conversion rate로 해석하기에는 이르다.
- 광고 재개 후 paid traffic 기준으로 같은 row 확인이 필요하다.
