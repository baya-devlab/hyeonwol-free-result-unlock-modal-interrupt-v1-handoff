# 현월 무료 결과페이지 v1.1 Visual Polish Handoff

Generated: 2026-06-23 KST

Preview URL:
https://hyeonwol-free-result-interrupt-v1-rjj2de25m.vercel.app/

Mobile QA URL:
https://hyeonwol-free-result-interrupt-v1-rjj2de25m.vercel.app/?preview=1&free=1&freePersona=%EB%B6%89%EC%9D%80%20%EC%9E%A5%EB%AF%B8%ED%98%95&hidden=%EB%B6%89%EC%9D%80%20%EA%B2%BD%EA%B3%A0%EB%93%B1%ED%98%95

## Summary

This handoff documents the v1.1 visual polish pass for the pre-unlock free result page. The work improves the upper-page flow and visual hierarchy without changing production, payment, Meta ads, OpenAI calls, or `src/saju/*`.

## Before / After Section Order

Before:

1. Hero
2. Face dohwa overview
3. Saju pillar table
4. Origin summary
5. Face dohwa card
6. Public face dohwa explanation
7. Professional locked area
8. Bottom unlock gate

After:

1. Hero
2. Face dohwa overview
3. Face dohwa card
4. Integrated origin + saju pillar section
5. Public face dohwa explanation
6. Professional locked area
7. Bottom unlock gate

## Main Changes

### Face Dohwa Card Moved Up

The face dohwa card now appears before the origin/saju explanation. This gives the user a stronger visual reward earlier, before the page moves into text/table-based reasoning.

Affected code:

- `src/main.js`
  - `renderResult()`
  - `renderShareCardPreview()`

### Integrated Origin + Saju Section

The previous separate `#free-pillar-table` and `#free-origin-summary` sequence has been consolidated visually. The `#free-origin-summary` section now contains an embedded `#free-pillar-table` anchor so existing section reach tracking can still find the saju pillar section.

The integrated structure:

1. `왜 이렇게 나왔는가` chip
2. `원국은 이미 한쪽을 가리키고 있습니다.`
3. Intro copy about 월지 / 일간 / 일지
4. Saju pillar table
5. Compact 월지 / 일간 / 일지 summary rows
6. Short conclusion pointing to the assigned face dohwa type

Affected code:

- `src/main.js`
  - `renderSajuOriginSummary()`
  - `renderSajuPillarTable(id, { embedded: true })`

Affected styles:

- `src/styles.css`
  - `.free-origin-integrated`
  - `.origin-summary-body`
  - `.saju-pillar-table-embed`
  - `.origin-summary-grid`

### Reduced Box-In-Box Feeling

The integrated origin section no longer uses the heavy `report-chapter reveal-card saju-origin-card` wrapper. The outer panel is now visually lighter, while the saju table itself remains card-like for readability.

### Face Overview Cards Strengthened

The face overview cards keep the same copy and three concepts:

- 첫인상
- 남는 방식
- 오해 포인트

The layout is now more diagnostic:

- `01 첫인상` is a larger lead card.
- `02 남는 방식` and `03 오해 포인트` sit below as secondary cards.
- On narrow mobile widths, the secondary cards stack with a slight offset instead of forcing a cramped two-column layout.

Affected styles:

- `.face-overview-grid`
- `.face-overview-card`
- `.face-overview-card-1`
- `.face-overview-card-2`
- `.face-overview-card-3`

### Auto Modal Trigger Preserved

The unlock choice modal behavior is preserved:

- Auto-opens once when entering `#professional-locked-area`
- Does not open around the face card or integrated origin section
- Does not auto-reopen after closing in the same session
- Can be reopened manually from the bottom gate
- Does not auto-open in post-share/unlocked state

## QA Results

Commands:

- `npm run check`: PASS
- `npm run check:api`: PASS
- `npm run check:launch`: PASS

Fixture result:

- ready: 34
- passed: 34
- failed: 0
- unsupported: 2

Mobile viewports:

- 360x740: PASS
- 375x812: PASS
- 390x844: PASS
- 430x932: PASS

Face dohwa type QA:

- 붉은 장미형: PASS
- 차가운 달빛형: PASS
- 첫눈의 뮤즈형: PASS
- 무심한 고양이형: PASS
- 복숭아 안개형: PASS
- 검은 향수형: PASS
- 햇살 플러팅형: PASS
- 푸른 불꽃형: PASS

Preview QA:

- Section order: PASS
- Face dohwa card appears before saju/origin: PASS
- Saju/origin visually integrated: PASS
- `#free-pillar-table` preserved inside `#free-origin-summary`: PASS
- Face overview cards responsive at 360px: PASS
- Rule-based personalized public copy preserved: PASS
- No repeated blur before professional locked area: PASS
- Auto modal appears at locked area: PASS
- Auto modal does not reopen after close in same session: PASS
- Manual bottom gate reopens modal: PASS
- Post-share/unlocked state does not auto-open modal: PASS
- Console errors on Preview: 0
- Broken images on Preview: 0

## Generated Artifacts

- `screenshots/free-result-unlock-modal-interrupt-v1-1-visual-polish/`
- `screenshots/montage/free-result-unlock-modal-interrupt-v1-1-visual-polish-montage.png`
- `json/free-result-unlock-modal-interrupt-v1-1-qa.json`

## Risk Status

- Production deployed: no
- Real payment executed: no
- Test payment executed: no
- PortOne payment window opened: no
- Meta write executed: no
- OpenAI call executed: no
- `src/saju/*` changed: no

## Remaining Risks

- This is a Preview/Staging implementation. Production still requires a separate explicit approval and production QA.
- The integrated origin section preserves anchors/selectors, but downstream analytics should still be monitored after production promotion.
- Final UX judgment should be made on a real mobile device because screenshots cannot fully represent scroll rhythm.

