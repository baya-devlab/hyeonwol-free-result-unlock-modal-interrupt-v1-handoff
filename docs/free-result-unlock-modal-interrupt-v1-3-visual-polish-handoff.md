# 현월 무료 결과페이지 해금 전 Preview v1.3 Visual Polish Handoff

## 1. 링크

- Preview URL: https://hyeonwol-free-result-interrupt-v1-aq0wbuw5p.vercel.app/
- 모바일 QA URL: https://hyeonwol-free-result-interrupt-v1-aq0wbuw5p.vercel.app/?preview=1&free=1&freePersona=%EB%B6%89%EC%9D%80%20%EC%9E%A5%EB%AF%B8%ED%98%95&hidden=%EB%B6%89%EC%9D%80%20%EA%B2%BD%EA%B3%A0%EB%93%B1%ED%98%95
- Screenshot montage raw URL: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/montage/free-result-unlock-modal-interrupt-v1-3-visual-polish-montage.png
- DOM summary raw URL: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-3-dom-summary.json
- QA JSON raw URL: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-3-qa.json

## 2. 한 줄 결론

무료 결과페이지 해금 전 v1.2 구조는 유지하면서, 겉도화 개요 카드의 glossy/raised 표현, 한자 존재감, 예전 공유 버튼 스타일, 원국 하단 삼각 순환 다이어그램을 v1.3 Preview에 반영했다.

## 3. 변경 요약

### 겉도화 개요

- 2번 카드 제목을 `기억에 남는 지점`에서 `잔상`으로 변경했다.
- 3개 카드 모두 dark romance 톤의 glossy / embossed / raised card 느낌으로 강화했다.
- 카드 내부 한자 크기를 키우고, 제목 화면에서 쓰는 `Shilla_Culture(B)` / `Shilla Culture Title` 계열 폰트 스택을 반영해 더 예스럽고 붓글씨에 가까운 무드로 조정했다.

### 겉도화 카드 섹션 버튼

- `친구에게 공유하기` 버튼을 예전 분기형 퍼널 도입 전후 히스토리에서 쓰던 `primary-button kakao-share-button` 스타일로 복원했다.
- 근거: repo history상 v1.1 이전 커밋들(예: `9d2acf6`, `5ce6b41`)에서 `renderShareCardPreview()`는 `primary-button kakao-share-button` + `renderKakaoBubbleIcon()` 조합을 사용했고, 다운로드는 `secondary-button`이었다.
- `이미지 저장하기` 버튼은 예전처럼 `secondary-button` 계열을 유지했다.

### 왜 이렇게 나왔는가

- 원국 표 아래 월지/일간/일지 3카드를 겉도화 개요 카드와 겹치지 않도록 제거하고, 장식적 삼각 순환 다이어그램으로 교체했다.
- 노드 3개는 월지 -> 일간 -> 일지 흐름을 만들며, 각 노드의 한자/텍스트 의미는 유지했다.
- 섹션 외곽 구조는 유지하고, 내부 시각화가 과도하게 공학적이지 않도록 금색 점선 화살표와 어두운 광택 노드를 사용했다.

## 4. 유지한 것

- 해금 전 섹션 순서 유지: 히어로 -> 겉도화 개요 -> 겉도화 카드 -> 통합 원국 섹션 -> 겉도화 공개 해석 -> 전문 잠금 영역 -> 하단 게이트
- 자동 모달 동작 유지: 전문 잠금 영역 진입 시 1회 자동 노출, 닫은 뒤 자동 재노출 없음, 하단 CTA 수동 재오픈 가능
- post-share/unlocked 상태에서 자동 모달 미노출 유지
- rule-based 개인화 카피 유지
- `src/saju/*` 및 만세력 계산 로직 수정 없음
- Production 배포 없음, 실제/테스트 결제 없음, Meta/Kakao/Payment 설정 변경 없음

## 5. QA 결과

| 항목 | 결과 |
| --- | --- |
| 8개 겉도화 유형 QA | PASS (8/8) |
| 모바일 viewport QA | PASS (360x740, 375x812, 390x844, 430x932) |
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
BASE_URL='https://hyeonwol-free-result-interrupt-v1-aq0wbuw5p.vercel.app/' NODE_PATH=/tmp/hyeonwol-free-result-interrupt-v1/node_modules node /tmp/qa-v13.js
```

`check:launch` fixture 결과: 34 passed / 34 ready, unsupported 2, failed 0.

## 6. DOM / 섹션 구조 요약

| 순서 | selector | heading/chip | top | height |
| ---: | --- | --- | ---: | ---: |
| 1 | `#judgment` | 가명님의 겉도화는 | 0 | 690 |
| 2 | `#face-overview` | 겉도화 개요 | 708 | 843 |
| 3 | `#share` | 당신의 겉도화 | 1569 | 693 |
| 4 | `#free-origin-summary` | 왜 이렇게 나왔는가 | 2281 | 814 |
| 5 | `#face-dohwa-explanation` | 겉도화 해석 | 3113 | 783 |
| 6 | `#professional-locked-area` | 아직 닫힌 해석이 남아 있습니다 | 3914 | 545 |
| 7 | `#share-unlock` | 전문은 여기서 멈춰 있습니다 | 4481 | 445 |

## 7. 시각 자료

- Montage: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/montage/free-result-unlock-modal-interrupt-v1-3-visual-polish-montage.png
- Full long screenshot: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-3-visual-polish/01-full-long-390px.png
- Hero: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-3-visual-polish/02-hero.png
- Face overview: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-3-visual-polish/03-face-overview.png
- Face card/buttons: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-3-visual-polish/04-face-card.png
- Integrated origin cycle: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-3-visual-polish/05-integrated-origin.png
- Public face explanation: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-3-visual-polish/06-face-public.png
- Locked area: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-3-visual-polish/07-locked-area.png
- Auto modal: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-3-visual-polish/08-auto-modal.png

## 8. 남은 리스크

- 예전 버튼 디자인은 repo history에서 확인 가능한 `primary-button kakao-share-button` 조합으로 복원했다. 사용자가 기억하는 특정 캡처의 미세한 색감과 100% 동일한지는 최종 모바일 눈검수가 필요하다.
- 원국 삼각 순환 다이어그램은 360/375/390/430px에서 QA 통과했지만, 더 긴 사용자명이나 다른 기기 브라우저 UI 환경에서는 섹션 높이가 약간 달라질 수 있다.

## 9. ChatGPT가 보면 좋은 질문

- 겉도화 개요의 glossy card가 충분히 고급스럽고, 과하게 게임 UI처럼 보이지 않는가?
- 원국 삼각 순환 다이어그램이 "근거가 연결되어 하나의 유형이 된다"는 느낌을 주는가?
- 겉도화 카드 섹션의 예전 공유/저장 버튼 위계가 현재 분기형 퍼널 UX와 충돌하지 않는가?
