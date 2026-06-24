# 현월 Production 이벤트 Readiness 및 광고 재개 GO/NO-GO

## 1. 결론 요약

- 판정: **CONDITIONAL_GO**
- 허용 범위: **소액/부분 광고 재개만 권장**
- 금지/보류: 풀예산 재개, 대규모 구매 최적화 캠페인, 이벤트명별 Admin 확인 전 강한 성과 판단
- 핵심 이유: Production UX와 analytics endpoint 200은 확인됐지만, Admin 인증 없이 이벤트명별 DB row를 직접 확인하지 못했다.

## 2. 확인 범위

| 항목 | 결과 |
| --- | --- |
| Production URL | https://hyeonwol.dasi.ing/ |
| Production deployment | `dpl_8FgERhSxNt2uBe4JWnbosKwZ7uos` |
| Rollback target | `dpl_55zDkYJkCvZQCTM2zPE2Qv2zzWkv` |
| Admin status | configured, unauthenticated |
| Supabase status | configured according to `/api/admin/me` |
| Meta status | configured according to `/api/admin/me` |
| Admin metrics direct read | 401, expected auth gate |
| Vercel function logs | `/api/t/e`, `/api/t/s`, `/api/t/i` all observed with 200 |

## 3. 이벤트 수신 확인

| event_name | observed | source | latest_timestamp_kst | count_recent_window | confidence | notes |
| --- | --- | --- | --- | --- | --- | --- |
| `free_result_view` | inferred_yes | Production UX QA + `/api/t/e` 200 + code path | recent endpoint window | event-name count unavailable | medium | 무료 결과 도달 및 analytics endpoint 200 확인 |
| `unlock_choice_modal_open` | inferred_yes | Production UX QA + `/api/t/e` 200 + code path | recent endpoint window | event-name count unavailable | medium | 도화 지표 자동 모달 확인 |
| `unlock_choice_pay_select` | inferred_yes | Production UX QA + `/api/t/e` 200 + code path | recent endpoint window | event-name count unavailable | medium_low | 990원 직접 열람 선택 모달까지 확인 |
| `unlock_choice_share_select` | not_verified | not executed | - | - | low | 외부 카카오 공유 발송 리스크를 피하기 위해 최종 share select는 누르지 않음 |
| `unlock_granted` | not_verified | not executed | - | - | low | post-share 상태 QA는 했지만 새 unlock event 생성은 하지 않음 |
| `speed_dohwa_decode_payment_start` | not_verified | payment modal only | - | - | low | 실제 PG/주문 생성 단계로 넘어가는 pay button은 누르지 않음 |
| `speed_dohwa_decode_purchase_success` | not_checked | no payment completion | - | - | low | 실제/테스트 결제 금지로 미확인 |

## 4. Endpoint 로그 근거

최근 1시간 Vercel logs dedupe 기준:

| endpoint | count | status |
| --- | ---: | --- |
| `/api/t/e` | 17 | 200 |
| `/api/t/s` | 5 | 200 |
| `/api/t/i` | 1 | 200 |
| `/api/payment/config` | 4 | 200 |
| `/api/admin/me` | 1 | 200 |
| `/api/admin/metrics/events` | 1 | 401 expected |

주의: Vercel logs는 request body를 보여주지 않으므로 event_name별 row 확인은 아니다.

## 5. 핵심 퍼널 집계

이번 run에서는 event-name별 Admin/DB 집계가 불가능했다.

| 구간 | 집계 가능 여부 | 비고 |
| --- | --- | --- |
| `free_result_view -> unlock_choice_modal_open` | 제한적 | UX/code path/endpoint 200으로 추정 가능 |
| `unlock_choice_modal_open -> share_select` | 불가 | share select 미실행 |
| `unlock_choice_modal_open -> pay_select` | 제한적 | pay select UX는 확인, row 직접 확인 불가 |
| `free_result_view -> unlock_granted` | 불가 | unlock_granted 미생성 |
| `free_result_view -> payment_start` | 불가 | payment_start 미생성 |

데이터 충분성: **insufficient for final performance judgment**

## 6. Source-of-truth 상태

| 항목 | 상태 |
| --- | --- |
| current local deploy branch | `feature/free-result-unlock-modal-interrupt-v1` |
| current commit | `abf4784b2b93e635c8692b8d2e5dc0d997de56d7` |
| deployed source dirty files | `src/main.js`, `src/styles.css`, `docs/payment-live-readiness-latest.json` |
| source repo main | `/Users/daawony_/Documents/오두막/dowhadoryung-hyeonwol`, `main`, `88ea5ad` |
| pushed/merged | production state not merged to main |
| source_of_truth_status | `needs_commit` |

권장 후속 작업: 사용자가 Production 상태를 승인하면 `src/main.js`, `src/styles.css` 변경을 source repo에 commit/push/PR로 정리한다. generated JSON은 별도 판단.

## 7. GO/NO-GO 판정

판정: **CONDITIONAL_GO**

이유:

- Production URL, 핵심 UX, 자동 모달, 수동 CTA, post-share 상태, 990원 모달은 직전 post-deploy QA에서 PASS.
- Vercel logs에서 analytics endpoints가 200으로 수신되는 것은 확인.
- 하지만 Admin/DB에서 이벤트명별 수신 row를 직접 보지 못했다.
- `unlock_choice_share_select`, `unlock_granted`, `speed_dohwa_decode_payment_start`는 이번 run에서 생성/확인하지 않았다.
- Source-of-truth도 아직 commit 정리가 필요하다.

## 8. 광고 재개 가능 범위

권장: **소액/부분 재개**

- 기존 캠페인 전체/풀예산 재개는 보류.
- 먼저 Core 또는 screening 중 일부만 낮은 예산으로 재개.
- 첫 24시간은 ROAS보다 이벤트 수신과 중간 퍼널을 본다.

권장 시작 방식:

1. Day 0: 이 리포트 확인 후 광고 관리자에서 수동으로 일부만 ON.
2. Day 1: 소액 재개. 권장 총액은 기존 계획 대비 25~40% 수준.
3. Day 1~2: `free_result_view -> select`, `unlock_granted`, `payment_start` 확인.
4. Day 2~3: 이벤트 row가 Admin에서 확인되면 예산 유지/소폭 증액.

## 9. 첫 24~48h 기준 지표

우선순위:

1. `free_result_view`
2. `unlock_choice_modal_open`
3. `unlock_choice_share_select + unlock_choice_pay_select`
4. `unlock_granted`
5. `speed_dohwa_decode_payment_start`
6. `orders.status=PAID`

중단 기준:

- Production event endpoint 4xx/5xx 발생
- `free_result_view`는 있는데 select가 거의 없음
- `payment_start`가 계속 0
- 특정 광고가 클릭은 쓰는데 `free_result_view`가 현저히 낮음
- Admin에서 이벤트명별 row가 계속 확인되지 않음

증액 기준:

- `free_result_view -> any_select`가 의미 있게 발생
- `payment_start` 발생
- 990원 paid order 발생
- CPC/CTR이 나쁘지 않고 UX 퍼널도 같이 따라옴

## 10. 금지 작업 수행 여부

| 항목 | 수행 여부 |
| --- | --- |
| 실제 결제 | 하지 않음 |
| 테스트 결제 | 하지 않음 |
| Meta write | 하지 않음 |
| 광고 ON/OFF | 하지 않음 |
| 예산 변경 | 하지 않음 |
| DB schema 변경 | 하지 않음 |
| source repo commit/push | 하지 않음 |
| env 변경 | 하지 않음 |

## 11. 남은 리스크

- Admin 인증 없이는 이벤트명별 row-level 확인이 불가능하다.
- `speed_dohwa_decode_payment_start`는 실제 pay button click 직후 발생하므로, 결제 시작 전 단계만 보는 QA에서는 직접 확인되지 않는다.
- Production 배포 상태가 아직 GitHub source-of-truth에 정리되어 있지 않다.

## 12. 다음 추천 작업

1. 사용자가 Admin에 로그인해 최근 이벤트에서 `unlock_choice_modal_open`, `unlock_choice_pay_select`, `speed_dohwa_decode_payment_start`가 보이는지 확인한다.
2. Production 상태 승인 후 source repo commit/push/PR 정리.
3. 광고는 소액/부분 재개 후 24시간 안에 이벤트 row 재검증.
