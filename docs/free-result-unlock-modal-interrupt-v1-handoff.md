# 현월 무료 결과페이지 해금 전 구조 개편 v1 Handoff

## 목적

최근 `free_result_view -> unlock_choice_modal_open` 전환율이 약 37.5% 수준이라, 초반 블러/공유 요구를 줄이고 무료 결과 전반부에서 충분히 몰입시킨 뒤 후반부에서 전문 열람 선택 모달을 자동 1회 노출하는 실험입니다.

## Preview

- Preview URL: https://hyeonwol-free-result-interrupt-v1-5l4bxgbj9.vercel.app/
- 대표 모바일 QA URL: https://hyeonwol-free-result-interrupt-v1-5l4bxgbj9.vercel.app/?preview=1&free=1&freePersona=%EB%B6%89%EC%9D%80%20%EC%9E%A5%EB%AF%B8%ED%98%95&hidden=%EB%B6%89%EC%9D%80%20%EA%B2%BD%EA%B3%A0%EB%93%B1%ED%98%95

## 구현 구조

1. 히어로
   - `{name}님의 겉도화는 -> {personaName} -> oneLine -> keywords -> verdict`
   - `나왔습니다`, `현월의 판정`, `현월이 본 건` 제거

2. 겉도화 한 줄 판정
   - `겉도화 개요` chip
   - 첫인상 / 남는 방식 / 오해 포인트 3카드
   - 유형 map + 월지/일지/일간 오행 map 기반 rule-based 개인화

3. 사주원국 근거 요약
   - `왜 이렇게 나왔는가` chip
   - 사주원국 표 유지
   - 월지/일간/일지 요약 카드
   - 블러 없음

4. 겉도화 카드
   - 기존 카드 유지
   - 카드 저장 버튼 유지
   - 친구 공유 버튼은 ghost/outline 계열로 위계 하향

5. 겉도화 해석 공개부
   - 블러 없이 유형별 기본 본문 노출
   - 월지/일간/일지 오행 기반 개인화 블록 추가
   - 990원/속도화/결제 예고 없음

6. 전문 열람 선택 모달 자동 1회
   - 잠긴 전문 영역 30% 이상 진입 시 자동 노출
   - `sessionStorage` key: `hyeonwol_unlock_choice_auto_shown`
   - 닫으면 같은 세션에서 자동 재노출 없음
   - 수동 `전문 열람하기` CTA로는 다시 열림
   - post-share/unlocked 상태에서는 자동 노출 없음

7. 잠긴 전문 영역 + 최하단 게이트
   - 반복 블러 대신 잠긴 항목 카드 3개로 남은 전문 범위 제시
   - CTA: `전문 열람하기`

## QA 결과

- `npm run check`: PASS
- `npm run check:api`: PASS
- `npm run check:launch`: PASS
- fixture: ready 34 / passed 34 / failed 0 / unsupported 2
- Playwright mobile QA: 8 personas PASS
- Viewports: 360x740, 375x812, 390x844, 430x932 PASS
- Preview URL smoke QA: PASS
- console errors: 0
- broken images: 0
- real/test payment: not performed
- Meta changes: none
- production service deploy: none

## 주요 파일

- `src/main.js`: pre-unlock free result render path, rule-based copy maps, auto unlock choice modal trigger
- `src/styles.css`: overview cards, origin summary, public reading block, professional locked area, modal refinements
- `json/free-result-unlock-modal-interrupt-v1-qa.json`: QA result
- `screenshots/montage/free-result-unlock-modal-interrupt-v1-montage.png`: visual montage

## Notes for ChatGPT

이 실험의 성공 판단은 modal open 상승만 보면 안 됩니다. 자동 모달 때문에 open은 상승할 수 있으므로 다음도 함께 봐야 합니다.

- `unlock_choice_modal_open -> unlock_choice_share_select`
- `unlock_choice_modal_open -> unlock_choice_pay_select`
- `unlock_choice_modal_open -> close`
- `free_result_view -> unlock_granted`
- `free_result_view -> speed_dohwa_decode_payment_start`
- `free_result_view -> speed_dohwa_decode_purchase_success`

후속 분석에서는 자동 모달 source/context를 분리해서 manual CTA와 비교해야 합니다.
