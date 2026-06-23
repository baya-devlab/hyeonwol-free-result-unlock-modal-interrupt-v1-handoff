# 현월 무료 결과페이지 해금 전 Preview v1.4 Visual Polish Handoff

## 1. 링크

- Preview URL: https://hyeonwol-free-result-interrupt-v1-52kaastn3.vercel.app/
- 모바일 QA URL: https://hyeonwol-free-result-interrupt-v1-52kaastn3.vercel.app/?preview=1&free=1&freePersona=%EB%B6%89%EC%9D%80%20%EC%9E%A5%EB%AF%B8%ED%98%95&hidden=%EB%B6%89%EC%9D%80%20%EA%B2%BD%EA%B3%A0%EB%93%B1%ED%98%95
- Screenshot montage raw URL: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/montage/free-result-unlock-modal-interrupt-v1-4-visual-polish-montage.png
- DOM summary raw URL: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-4-dom-summary.json
- QA JSON raw URL: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-4-qa.json

## 2. 한 줄 결론

무료 결과페이지 해금 전 v1.3 구조를 유지하면서, 원국 순환 다이어그램 화살표를 더 독립적으로 정리하고, LOCKED 섹션 뒤에 도화 지표 / 겉도화 해석 전문 / 원국 해석 전문 3개 잠김 preview 섹션을 복원했다.

## 3. 변경 요약

### 왜 이렇게 나왔는가

- 월지 / 일간 / 일지 노드 3개는 유지했다.
- 시계방향 순환 구조는 유지하되, 화살표 path를 짧은 독립 화살표 3개로 조정했다.
- 화살표의 시작/끝이 노드 중심을 관통하지 않고, 노드 바깥 테두리 부근을 가리키도록 정리했다.
- 트라이앵글 아래 결론 문구는 두 블록처럼 보이지 않도록 하나의 `origin-summary-conclusion` 문단으로 합쳤다.

### LOCKED 섹션 이후 전문 preview 복원

LOCKED 전문 섹션 아래, 하단 게이트 위에 아래 3개 섹션을 추가했다.

1. 도화 지표: 기존 `renderDohwaIndicators()`의 locked 상태를 재사용하고 전체 지표를 블러 처리했다.
2. 겉도화 해석 전문: 기존 겉도화 해석 copy/tone을 사용하되 전문 preview body 전체를 블러 처리했다.
3. 원국 해석 전문: 기존 `renderSajuOriginReading()`의 원국 해석 내용을 재사용하되, 이 하단 preview에서는 본문 전체를 블러 처리했다.

각 섹션 overlay CTA 문구는 `전문 보기`로 통일했다.

## 4. 유지한 것

- v1.3의 겉도화 개요 glossy 카드, `잔상` 명칭, 공유/저장 버튼 복원 스타일 유지
- 해금 전 기본 섹션 순서 유지: 히어로 -> 겉도화 개요 -> 겉도화 카드 -> 통합 원국 섹션 -> 겉도화 공개 해석 -> LOCKED -> 잠긴 전문 preview 3개 -> 하단 게이트
- 자동 모달 동작 유지: LOCKED 섹션 진입 시 1회 자동 노출, 닫은 뒤 자동 재노출 없음, 하단 CTA 수동 재오픈 가능
- post-share/unlocked 상태에서 자동 모달 미노출 유지
- rule-based 개인화 카피 유지
- `src/saju/*` 및 만세력 계산 로직 수정 없음
- Production 배포 없음, 실제/테스트 결제 없음, Meta/Kakao/Payment 설정 변경 없음

## 5. QA 결과

| 항목 | 결과 |
| --- | --- |
| 8개 겉도화 유형 QA | PASS (8/8) |
| 모바일 viewport QA | PASS (360x740, 375x812, 390x844, 430x932) |
| 새 locked 전문 preview 3개 | PASS |
| overlay CTA `전문 보기` | PASS |
| console error | 0 |
| broken image | 0 |
| horizontal overflow | 0 |
| 자동 모달 1회 노출 | PASS |
| 닫은 뒤 자동 재노출 없음 | PASS |
| 하단 CTA 수동 재오픈 | PASS |
| post-share/unlocked 자동 모달 없음 | PASS |

검증 커맨드:

```bash
npm run check
npm run check:api
npm run check:launch
git diff --check
BASE_URL='https://hyeonwol-free-result-interrupt-v1-52kaastn3.vercel.app/' NODE_PATH=/tmp/hyeonwol-free-result-interrupt-v1/node_modules node /tmp/qa-v14.js
```

`check:launch` fixture 결과: 34 passed / 34 ready, unsupported 2, failed 0.

## 6. DOM / 섹션 구조 요약

| 순서 | selector | heading/chip | top | height |
| ---: | --- | --- | ---: | ---: |
| 1 | `#judgment` | 가명님의 겉도화는 | 0 | 690 |
| 2 | `#face-overview` | 겉도화 개요 | 708 | 843 |
| 3 | `#share` | 당신의 겉도화 | 1569 | 693 |
| 4 | `#free-origin-summary` | 왜 이렇게 나왔는가 | 2281 | 780 |
| 5 | `#face-dohwa-explanation` | 겉도화 해석 | 3078 | 783 |
| 6 | `#professional-locked-area` | 아직 닫힌 해석이 남아 있습니다 | 3879 | 545 |
| 7 | `#indicators` | 도화 지표 | 4444 | 802 |
| 8 | `#locked-face-dohwa-professional` | 겉도화 해석 전문 | 5263 | 567 |
| 9 | `#free-origin-reading` | 원국은 이미 한쪽을 가리키고 있습니다. | 5846 | 702 |
| 10 | `#share-unlock` | 전문은 여기서 멈춰 있습니다 | 6569 | 445 |

## 7. 잠긴 전문 preview 섹션

| id | chip/heading | overlay | blur |
| --- | --- | --- | --- |
| `indicators` | 도화 지표 | 전문 보기 | yes |
| `locked-face-dohwa-professional` | 겉도화 해석 전문 | 전문 보기 | yes |
| `free-origin-reading` | 원국 해석 | 전문 보기 | yes |

## 8. 시각 자료

- Montage: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/montage/free-result-unlock-modal-interrupt-v1-4-visual-polish-montage.png
- Full long screenshot: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-4-visual-polish/01-full-long-390px.png
- Origin cycle: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-4-visual-polish/05-integrated-origin.png
- Locked indicators: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-4-visual-polish/08-locked-indicators.png
- Locked face professional: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-4-visual-polish/09-locked-face-professional.png
- Locked origin professional: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-4-visual-polish/10-locked-origin-professional.png
- Auto modal: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-4-visual-polish/12-auto-modal.png

## 9. 남은 리스크

- 새 잠긴 전문 preview 섹션 3개가 추가되면서 해금 전 페이지 길이는 v1.3보다 길어졌다. 의도된 변경이지만, 모바일에서 하단 게이트까지의 거리감은 실제 눈검수로 한 번 더 보는 것이 좋다.
- 이번 작업은 Preview/Staging 전용이며 production에는 반영하지 않았다.

## 10. ChatGPT가 보면 좋은 질문

- LOCKED 뒤에 복원된 3개 전문 preview가 충분히 “전문이 남아 있다”는 기대감을 주는가?
- 각 섹션의 `전문 보기` overlay가 너무 장사꾼처럼 보이지 않는가?
- 원국 순환 다이어그램의 화살표가 이제 독립된 방향 흐름으로 읽히는가?
