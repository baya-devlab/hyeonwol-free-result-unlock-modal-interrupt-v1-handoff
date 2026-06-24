# 현월 무료 결과페이지 v1.5 final CTA handoff

## 1. 기준 링크

- Preview URL: https://hyeonwol-free-result-interrupt-v1-31v7rip0c.vercel.app
- Mobile QA URL: https://hyeonwol-free-result-interrupt-v1-31v7rip0c.vercel.app/?preview=1&free=1&freePersona=%EB%B6%89%EC%9D%80%20%EC%9E%A5%EB%AF%B8%ED%98%95&hidden=%EB%B6%89%EC%9D%80%20%EA%B2%BD%EA%B3%A0%EB%93%B1%ED%98%95
- Screenshot montage: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/montage/free-result-unlock-modal-interrupt-v1-5-final-cta-montage.png
- DOM summary JSON: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-5-final-cta-dom-summary.json
- QA JSON: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-5-final-cta-qa.json

## 2. 이번 반영 내용

1. `왜 이렇게 나왔는가` 섹션의 원국표 아래 설명을 월지/일지/일간 개별 카드형 설명에서 산문형 리딩으로 정리했다.
2. 트라이앵글 아래 결론 문장에 `월지 → 일지 → 일간` 순서, `관계`, `전형적인` 표현을 포함했다.
3. 8개 겉도화 유형별 `personaRelationReason` rule-based map을 적용했다.
4. `겉도화 해석` 공개 본문 아래에 짧은 partial blur tail을 추가했다.
5. partial blur tail의 CTA 문구는 `🔒 전문 보기`이며, 클릭 시 기존 전문 열람 선택 모달을 연다.
6. partial blur tail 자체는 자동 모달 트리거가 아니다.
7. `도화 지표 전문 블러 → 겉도화 해석 전문 블러 → 원국 해석 전문 블러` 뒤에 최종 `LOCKED · 전문` CTA를 배치했다.
8. 사용자 화면에서 `LOCKED · 전문` CTA가 중복 노출되지 않도록 `#share-unlock`은 hidden anchor로만 보존했다.
9. 자동 모달은 최종 `#professional-locked-area` 진입 기준으로 1회만 노출되도록 유지했다.

## 3. 현재 해금 전 섹션 순서

1. 히어로
2. 겉도화 개요
3. 겉도화 카드
4. 왜 이렇게 나왔는가
5. 겉도화 해석 공개부 + partial blur tail
6. 도화 지표 전문 블러
7. 겉도화 해석 전문 블러
8. 원국 해석 전문 블러
9. LOCKED · 전문 최종 CTA

## 4. QA 결과 요약

- 모바일 viewport: 360x740, 375x812, 390x844, 430x932 확인
- 8개 겉도화 유형 smoke QA 확인
- console error: 0
- page error: 0
- broken image: 0
- horizontal overflow: 0
- partial blur tail height: 215px, 235px, 236px, 236px
- persona relation reason failure: 0
- partial blur tail 진입만으로 자동 모달 노출 없음
- partial blur tail CTA 클릭 시 모달 열림
- 최종 LOCKED CTA 진입 시 자동 모달 1회 노출
- 닫은 뒤 자동 재노출 없음
- 최종 CTA 수동 클릭으로 모달 재오픈 가능
- post-share/unlocked 상태 자동 모달 미노출

## 5. 섹션별 screenshot raw URL

- Full page 390px: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-5-final-cta/01-full-page-390.png
- Hero: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-5-final-cta/02-hero.png
- Face overview: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-5-final-cta/03-face-overview.png
- Face card: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-5-final-cta/04-face-card.png
- Origin summary: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-5-final-cta/05-origin-summary.png
- Public explanation + partial blur: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-5-final-cta/06-face-explanation-partial-blur.png
- Indicator blur: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-5-final-cta/07-indicators-blur.png
- Face professional blur: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-5-final-cta/08-face-professional-blur.png
- Origin professional blur: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-5-final-cta/09-origin-professional-blur.png
- Final LOCKED CTA: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-5-final-cta/10-final-locked-cta.png
- Auto unlock modal: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-5-final-cta/11-auto-unlock-modal.png

## 6. 변경하지 않은 것

- Production 배포: 안 함
- 실제 결제/테스트 결제: 안 함
- Meta/Kakao/Payment 설정 변경: 없음
- `src/saju/*` 및 만세력 계산 로직 수정: 없음
- OpenAI 호출: 없음
- 분기형 퍼널 결제/공유 로직 자체 변경: 없음

## 7. 남은 리스크

- 이번 작업은 Preview 기준 QA다. Production 반영 전에는 동일한 URL/환경 기준으로 한 번 더 smoke QA가 필요하다.
- partial blur tail의 본문은 기존 전문 문단 일부를 재사용한 미리보기 연출이다. 실제 해금 후 전문 내용과 완전히 동일한 위치/분량을 보장하는 구조는 아니다.
