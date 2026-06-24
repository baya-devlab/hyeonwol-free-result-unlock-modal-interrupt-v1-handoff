# 현월 무료결과페이지 v1.5 Stable QA URL + 도화 지표 자동 모달 Handoff

## 1. 결론 요약

- Stable QA URL: https://hyeonwol-free-result-interrupt-v1-qa.vercel.app
- Stable mobile QA URL: https://hyeonwol-free-result-interrupt-v1-qa.vercel.app/?preview=1&free=1&freePersona=%EB%B6%89%EC%9D%80%20%EC%9E%A5%EB%AF%B8%ED%98%95&hidden=%EB%B6%89%EC%9D%80%20%EA%B2%BD%EA%B3%A0%EB%93%B1%ED%98%95
- Immutable Preview URL: https://hyeonwol-free-result-interrupt-v1-7m2tir94p.vercel.app
- Immutable mobile QA URL: https://hyeonwol-free-result-interrupt-v1-7m2tir94p.vercel.app/?preview=1&free=1&freePersona=%EB%B6%89%EC%9D%80%20%EC%9E%A5%EB%AF%B8%ED%98%95&hidden=%EB%B6%89%EC%9D%80%20%EA%B2%BD%EA%B3%A0%EB%93%B1%ED%98%95
- Production 배포: 하지 않음
- 실제/테스트 결제: 하지 않음
- Meta/Kakao/Payment 설정 변경: 없음
- `src/saju/*` 및 만세력 계산 로직 수정: 없음

이번 작업은 QA 편의성을 위해 stable non-production Vercel alias를 최신 Preview deployment에 연결하고, 자동 전문 열람 선택 모달의 자동 트리거를 최종 `LOCKED · 전문` CTA가 아니라 `도화 지표` 섹션 기준으로 앞당긴 버전입니다.

## 2. Stable QA URL 설정

| 항목 | 값 |
| --- | --- |
| 방식 | Vercel alias |
| Stable alias | `hyeonwol-free-result-interrupt-v1-qa.vercel.app` |
| 연결 대상 | `hyeonwol-free-result-interrupt-v1-7m2tir94p.vercel.app` |
| 연결 명령 | `vercel alias set hyeonwol-free-result-interrupt-v1-7m2tir94p.vercel.app hyeonwol-free-result-interrupt-v1-qa.vercel.app` |
| Production domain 영향 | 없음 |
| `hyeonwol.dasi.ing` 변경 | 없음 |

`vercel inspect hyeonwol-free-result-interrupt-v1-qa.vercel.app` 결과, stable alias가 immutable Preview deployment `dpl_HwpKiF2jhwmXT4ofc4xrpptpihmB`를 가리키는 것을 확인했습니다.

## 3. 자동 모달 변경

| 항목 | 이전 | 변경 후 |
| --- | --- | --- |
| 자동 모달 트리거 | 최종 `LOCKED · 전문` CTA 영역 | `#indicators` 도화 지표 섹션 |
| trigger source | `auto_final_locked_area` | `dohwa_indicator_auto_gate` |
| 오픈 타이밍 | 최종 CTA 40% 내외 진입 | 도화 지표 제목/blur가 보인 뒤 약 420ms 지연 |
| 최종 CTA | 자동 트리거 포함 | 자동 트리거 제거, 수동 CTA 유지 |
| partial blur | 자동 모달 미노출 | 자동 모달 미노출 유지 |

구현상 `#indicators`에만 `data-auto-unlock-choice-trigger="dohwa_indicator_auto_gate"`가 존재합니다. 최종 `#professional-locked-area`에는 auto trigger attr이 없습니다.

## 4. 유지한 동작

- 자동 모달은 1회만 노출됩니다.
- 사용자가 닫으면 같은 세션에서 자동 재노출되지 않습니다.
- partial blur tail 진입만으로 자동 모달은 뜨지 않습니다.
- 도화 지표/진모습/원국 해석/최종 CTA의 수동 `전문 보기` CTA는 계속 modal을 엽니다.
- post-share/unlocked 상태에서는 자동 모달이 뜨지 않습니다.
- 최종 `LOCKED · 전문` CTA는 후반에 1회 유지됩니다.

## 5. QA 결과

| 항목 | 결과 |
| --- | --- |
| Stable QA URL 200 | PASS |
| Stable mobile QA URL 200 | PASS |
| Immutable Preview URL 200 | PASS |
| Immutable mobile QA URL 200 | PASS |
| `npm run check` | PASS |
| `npm run check:api` | PASS |
| `npm run check:launch` | PASS, fixture 34/34 passed |
| `git diff --check` | PASS |
| 모바일 viewport QA | 360 / 375 / 390 / 430 px PASS |
| 8개 겉도화 유형 smoke QA | PASS |
| partial blur 자동 모달 미노출 | PASS |
| 도화 지표 자동 모달 노출 | PASS |
| 수동 CTA 4종 modal open | PASS |
| post-share/unlocked 자동 모달 미노출 | PASS |
| console error | 0 |
| broken image | 0 |
| horizontal overflow | 0 |

## 6. Raw 자료

- Montage: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/montage/free-result-unlock-modal-interrupt-v1-5-stable-auto-modal-montage.png
- DOM summary: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-5-stable-auto-modal-dom-summary.json
- QA JSON: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-5-stable-auto-modal-qa.json
- Raw links index: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/raw-links.md

## 7. 남은 리스크

- Stable alias는 non-production Vercel alias입니다. 이후 새 Preview를 만들 때도 이 stable alias를 최신 deployment로 다시 연결하면 사용자는 같은 모바일 URL로 계속 QA할 수 있습니다.
- `vercel alias list`는 이번 `vercel.app` alias를 표에 표시하지 않았지만, `vercel alias set`, `curl 200`, `vercel inspect`로 연결을 확인했습니다.
- Production 배포나 실제 결제 테스트는 수행하지 않았습니다.
