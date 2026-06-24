# 현월 무료결과페이지 v1.5 stable-auto-modal Production 배포 및 post-deploy QA

## 1. 결론 요약

- Production 배포 완료: `https://hyeonwol.dasi.ing/`
- 새 Production deployment: `dpl_8FgERhSxNt2uBe4JWnbosKwZ7uos`
- 직전 Production rollback target: `dpl_55zDkYJkCvZQCTM2zPE2Qv2zzWkv`
- 핵심 QA 판정: PASS
- 실제 결제/테스트 결제/Meta write/광고 ON/DB schema 변경: 실행하지 않음

## 2. 기준 URL

| 항목 | URL |
| --- | --- |
| Production | https://hyeonwol.dasi.ing/ |
| Stable QA alias | https://hyeonwol-free-result-interrupt-v1-qa.vercel.app |
| Immutable Preview | https://hyeonwol-free-result-interrupt-v1-7m2tir94p.vercel.app |
| Stable handoff | https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/docs/free-result-unlock-modal-interrupt-v1-5-stable-auto-modal-handoff.md |

## 3. 배포 전 최소 확인

| 항목 | 결과 |
| --- | --- |
| 이전 Production deployment 기록 | `dpl_55zDkYJkCvZQCTM2zPE2Qv2zzWkv` |
| Production project 확인 | `dowhadoryung-hyeonwol` |
| `npm run check` | PASS |
| `npm run check:api` | PASS |
| `npm run check:launch` | PASS, mock payment readiness only |
| `git diff --check` | PASS |
| `src/saju/*` 변경 | 없음 |
| DB migration/schema 변경 | 없음 |
| Payment/Kakao/Meta env 변경 | 없음 |

## 4. Production 배포 정보

| 항목 | 값 |
| --- | --- |
| Deploy complete KST | 2026-06-24 15:41:52 KST |
| New deployment ID | `dpl_8FgERhSxNt2uBe4JWnbosKwZ7uos` |
| Deployment URL | https://dowhadoryung-hyeonwol-i5dz4nen0-bayas-projects-36f7157a.vercel.app |
| Production alias | https://hyeonwol.dasi.ing |
| Previous deployment ID | `dpl_55zDkYJkCvZQCTM2zPE2Qv2zzWkv` |
| Rollback command | `vercel rollback dpl_55zDkYJkCvZQCTM2zPE2Qv2zzWkv --yes` |

## 5. Production post-deploy QA

| 영역 | 결과 | 비고 |
| --- | --- | --- |
| Production URL 200 | PASS | `https://hyeonwol.dasi.ing/` |
| Mobile 390px render | PASS | Preview/result screen |
| Console error | PASS | 0 |
| Broken image | PASS | 0 |
| Horizontal overflow | PASS | 0 |
| 일반 입력 플로우 | PASS | 랜딩 -> 빠른 입력 -> 이메일 skip -> 무료 결과 도달 |
| 무료 결과페이지 주요 섹션 | PASS | 히어로, 겉도화 개요, 겉도화 카드, 원국, 겉도화 해석, 잠금 섹션 확인 |
| 자동 모달: partial blur | PASS | 겉도화 해석 partial blur 진입만으로 자동 모달 미노출 |
| 자동 모달: 도화 지표 | PASS | 도화 지표 구간에서 1회 노출 |
| 자동 모달 닫은 뒤 재노출 | PASS | 닫은 뒤 재스크롤해도 자동 재노출 없음 |
| post-share/unlocked 자동 모달 | PASS | `speedUnlocked=1` 상태에서 자동 트리거 0, 모달 미노출 |
| 수동 CTA | PASS | 5개 CTA 모두 unlock choice modal open |
| 카카오 공유 미리보기 | PASS | 미리보기 모달 열림, 생년월일 등 민감정보 미포함 |
| 이미지 저장 | PASS | 저장 toast 확인, console error 0 |
| 990원 결제 시작 | PASS | 결제 모달 직전/모달 도달, PortOne iframe 0, 결제 완료 미실행 |
| 이벤트/Admin/Analytics | NOT CHECKED | fast deploy QA 범위에서 DB/Admin/Meta 조회는 수행하지 않음 |

## 6. 수동 CTA QA 상세

| CTA source | 결과 |
| --- | --- |
| `face_dohwa_explanation_partial_blur_gate` | modal open |
| `dohwa_indicator_blur_gate` | modal open |
| `locked_face_dohwa_professional_gate` | modal open |
| `origin_reading_blur_gate` | modal open |
| `professional_locked_area` | modal open |

## 7. 8개 유형 smoke QA

8개 겉도화 유형 모두 PASS:

- 붉은 장미형
- 차가운 달빛형
- 첫눈의 뮤즈형
- 무심한 고양이형
- 복숭아 안개형
- 검은 향수형
- 햇살 플러팅형
- 푸른 불꽃형

각 유형에서 다음을 확인함:

- 유형명 표시
- 겉도화 개요
- 겉도화 카드
- 원국 섹션
- 겉도화 해석
- 도화 지표/진모습/전문 잠금 섹션
- broken image 0
- horizontal overflow 0
- initial modal false

## 8. Mobile viewport QA

| Viewport | 결과 |
| --- | --- |
| 360x740 | PASS |
| 375x812 | PASS |
| 390x844 | PASS |
| 430x932 | PASS |

## 9. 금지 작업 수행 여부

| 항목 | 수행 여부 |
| --- | --- |
| 실제 결제 | 하지 않음 |
| 테스트 결제 | 하지 않음 |
| Meta write | 하지 않음 |
| 광고 ON/OFF | 하지 않음 |
| 광고 예산 변경 | 하지 않음 |
| Payment/Kakao/Meta env 변경 | 하지 않음 |
| DB schema/migration 변경 | 하지 않음 |
| `src/saju/*` 수정 | 없음 |
| OpenAI 호출 | 하지 않음 |

## 10. Raw 자료

| 자료 | Raw URL |
| --- | --- |
| QA JSON | https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-5-production-post-deploy-qa.json |
| DOM summary | https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/json/free-result-unlock-modal-interrupt-v1-5-production-post-deploy-dom-summary.json |
| Screenshot montage | https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/screenshots/montage/free-result-unlock-modal-interrupt-v1-5-production-post-deploy-montage.png |
| Raw links | https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/raw-links-production-post-deploy-20260624.md |
| Manifest | https://raw.githubusercontent.com/baya-devlab/hyeonwol-free-result-unlock-modal-interrupt-v1-handoff/main/manifest-production-post-deploy-20260624.json |

## 11. 남은 리스크

- Admin/Analytics/Meta 이벤트 수신은 이번 fast deploy QA에서 직접 조회하지 않았다.
- 이미지 저장은 브라우저 런타임 download event로는 포착되지 않았지만, 앱 내부 저장 toast 및 console error 0을 확인했다.
- 실제 카카오 외부 발송은 하지 않았다. 공유 미리보기와 트리거 전 단계까지만 확인했다.

## 12. 다음 추천 작업

1. 사용자가 실기기로 Production 화면을 빠르게 확인한다.
2. 광고를 재개하기 전, 필요하면 Admin/Analytics read-only로 `unlock_choice_modal_open` / `unlock_choice_pay_select` 이벤트 수신만 확인한다.
3. 문제가 발견되면 직전 deployment `dpl_55zDkYJkCvZQCTM2zPE2Qv2zzWkv`로 rollback한다.
