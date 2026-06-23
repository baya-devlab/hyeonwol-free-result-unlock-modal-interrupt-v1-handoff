# 현월 무료 결과페이지 해금 전 Preview v1.2 Visual Polish Handoff

## 1. 결론

무료 결과페이지 해금 전 Preview v1.1 구조는 유지하면서, 모바일 QA 피드백을 반영해 v1.2 시각 polish를 적용했다.

- Production 배포: 하지 않음
- 실제/테스트 결제: 하지 않음
- Meta/Kakao/Payment 설정 변경: 하지 않음
- `src/saju/*` 및 만세력 계산 로직 변경: 하지 않음
- Preview URL: https://hyeonwol-free-result-interrupt-v1-5cmqlebmu.vercel.app/
- 모바일 QA URL: https://hyeonwol-free-result-interrupt-v1-5cmqlebmu.vercel.app/?preview=1&free=1&freePersona=%EB%B6%89%EC%9D%80%20%EC%9E%A5%EB%AF%B8%ED%98%95&hidden=%EB%B6%89%EC%9D%80%20%EA%B2%BD%EA%B3%A0%EB%93%B1%ED%98%95

## 2. 변경 요약

### 전반 공통

- 결과페이지 내 섹션 목차 라벨을 `world-label` 텍스트칩 스타일로 통일했다.
- v1.1의 기본 섹션 순서는 유지했다.

현재 해금 전 순서:

1. 히어로
2. 겉도화 개요
3. 겉도화 카드
4. 왜 이렇게 나왔는가 + 사주원국 통합 섹션
5. 겉도화 공개 해석
6. 전문 잠금 영역
7. 하단 게이트

### 히어로

- `붉은 장미형` 제목과 키워드칩 사이 여백을 줄였다.
- 히어로 verdict 문장에서 `제 눈엔,`을 제거했다.

### 겉도화 개요

- 3개 카드를 상하 정렬로 변경했다.
- 카드 제목을 변경했다.
  - `남는 방식` -> `기억에 남는 지점`
  - `오해 포인트` -> `오해`
- 각 카드가 실제 사주원국 글자 기반으로 다르게 보이도록 시각화했다.
  - 첫인상: 월지
  - 기억에 남는 지점: 일지
  - 오해: 일간
- 각 카드에는 큰 한자, 기준 위치, 오행 기반 컬러 무드가 들어간다.

### 겉도화 카드

- `친구에게 공유하기` 버튼을 v1.1의 ghost 스타일에서 기존 `secondary-button` 계열로 롤백했다.
- 카드 이미지/저장 버튼/섹션 위치는 유지했다.

### 왜 이렇게 나왔는가 + 사주원국 통합 섹션

- 섹션 전체 외곽 테두리/박스는 다시 보이게 했다.
- 사주원국표 자체를 감싸던 추가 박스감은 제거했다.
- 월지/일간/일지 요약 카드는 겉도화 개요 카드와 같은 `dohwa-basis-card` 비주얼 시스템을 사용한다.
- 텍스트 내용과 사주 계산값은 변경하지 않았다.

### 겉도화 해석

- 기존 일반 제목 `붉은 장미형은 어떻게 보이는가`를 제거했다.
- 기존 보조 설명 `겉도화는 내가 생각하는 내 모습이 아니라...`를 제거했다.
- 유형별 커스텀 문장을 메인 제목으로 사용한다.
  - 예: `붉은 장미형은 장면의 중심으로 남습니다`

## 3. 구현 파일

| 파일 | 변경 내용 |
| --- | --- |
| `src/main.js` | 히어로 문구 정리, 겉도화 개요 카드 데이터/마크업, 원국 통합 카드 마크업, 공유 버튼 클래스 롤백, 겉도화 해석 제목 변경 |
| `src/styles.css` | 텍스트칩 공통 스타일, 개인화 카드 비주얼, 히어로 간격, 원국 통합 섹션 박스/표 wrapper 정리 |
| `json/free-result-unlock-modal-interrupt-v1-2-qa.json` | Preview 기준 자동 QA 결과 |
| `json/free-result-unlock-modal-interrupt-v1-2-dom-summary.json` | 섹션/DOM/카드 구조 요약 |
| `screenshots/free-result-unlock-modal-interrupt-v1-2-visual-polish/` | 모바일 QA 섹션별 스크린샷 |
| `screenshots/montage/free-result-unlock-modal-interrupt-v1-2-visual-polish-montage.png` | ChatGPT 검토용 montage |

## 4. QA 결과

### 실행한 커맨드

| 명령 | 결과 |
| --- | --- |
| `npm run check` | PASS |
| `npm run check:api` | PASS |
| `npm run check:launch` | PASS, fixture 34/34 |
| `git diff --check` | PASS |
| Preview Playwright QA | PASS |

### Preview QA 범위

- 모바일 390px 기준 전체 흐름 QA: PASS
- 8개 겉도화 유형 QA: PASS
- 모바일 viewport 360/375/390/430 QA: PASS
- console error: 0
- broken image: 0
- horizontal overflow: 0
- 자동 모달: 전문 잠금 영역 진입 시 1회 노출 PASS
- 모달 닫은 뒤 자동 재노출 없음: PASS
- 수동 `전문 열람하기` CTA 재오픈: PASS
- post-share/unlocked 상태 자동 모달 미노출: PASS

## 5. 시각 검토용 자료

Public raw URL:

- Handoff doc: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/docs/free-result-unlock-modal-interrupt-v1-2-visual-polish-handoff.md
- Montage PNG: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/montage/free-result-unlock-modal-interrupt-v1-2-visual-polish-montage.png
- QA JSON: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-2-qa.json
- DOM summary JSON: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-2-dom-summary.json
- Full long screenshot: https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/free-result-unlock-modal-interrupt-v1-2-visual-polish/01-full-long-390px.png

## 6. ChatGPT가 봐야 할 포인트

1. 겉도화 개요 카드 3개가 이제 충분히 “진단 결과 카드”처럼 보이는지
2. 월지/일간/일지 기반 컬러/한자 비주얼이 과하거나 유치하지 않은지
3. `왜 이렇게 나왔는가` 통합 섹션이 다시 박스감은 가지되, 이중 박스 느낌은 줄었는지
4. 겉도화 해석의 유형별 제목 한 문장이 기존 제목/보조설명보다 더 몰입적인지
5. `친구에게 공유하기` 버튼 롤백 스타일이 현재 카드 섹션에 맞는지

## 7. 남은 리스크

- 이번 작업은 Preview/Staging 검수용이다. Production에는 반영하지 않았다.
- 이미지/문구의 최종 취향 판단은 사용자의 모바일 실기기 검수가 필요하다.
- `npm run check:launch`가 `docs/payment-live-readiness-latest.json`을 갱신했으나, 이번 작업 범위에는 포함하지 않는다.
