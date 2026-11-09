# Design System — Re:Source AI

작성일: 2026-11-09
미리보기: [docs/mockup/resource-ai-design-system-v3.html](docs/mockup/resource-ai-design-system-v3.html)

## 제품 맥락

- **무엇인가:** 폐기물 더미를 찍으면 에이전트 6개가 품목·오염도·규정·묶음 수거·비용·탄소를 판단하고 견적 요청서까지 만드는 웹 앱.
- **누가 쓰는가:** 산업단지 입주 중소 제조업체의 환경·총무 담당자. 시연 청중은 대회 심사위원.
- **분야:** 폐기물 관리, 순환자원, 탄소 회계. 참고한 제품은 Rubicon, AMP Robotics, Watershed(폐기물·ESG), Ramp, Mercury, Linear(핀테크·업무 도구).
- **형태:** 데스크톱 우선 웹 앱. 업로드 화면만 모바일 촬영을 고려한다.
- **기억시킬 한 가지:** 쓰레기가 돈이 된다.

## 미감 방향

- **방향:** 산업 원장(Industrial Ledger). 산업·실용 계열에 핀테크의 정밀함을 더한다. 증권 앱과 검사 성적서를 섞은 인상이다.
- **장식:** 최소. 모든 영역을 카드로 감싸지 않고 가는 구분선과 정렬된 행으로 구조를 만든다. 규정 체크리스트에만 영수증식 점선 리더를 쓴다.
- **분위기:** 폐기물 더미 하나하나를 시세가 붙은 상품처럼 다룬다. 화면의 절정은 손익 부호가 0을 넘는 순간이다.
- **하지 않는 것:** 초록 브랜드 색, 자연·나뭇잎 이미지, 보라 그라데이션, 아이콘 원형 3열 그리드, 이모지 아이콘, 에이전트 마스코트, 채팅 말풍선 UI.

### 근거 (리서치 요약)

폐기물·ESG 제품은 거의 모두 초록 계열과 자연 사진을 써서 서로 구별되지 않는다. 이 제품의 사용자는 처리비를 줄여야 하는 담당자이고 설득 대상은 손익을 보는 심사위원이므로, ESG가 아니라 핀테크 문법을 빌린다. 초록은 이익(+)이 생긴 숫자에만 아껴 쓴다.

## 서체

| 역할 | 글꼴 | 설정 |
|---|---|---|
| 제목·본문·UI | Wanted Sans Variable | 굵기로만 위계를 만든다 |
| 숫자 (금액, kg, tCO₂e, 시각, 신뢰도) | Geist Mono | `tabular-nums` 필수 |
| 코드 | Geist Mono | |

- **로딩:** 앱에서는 Wanted Sans 가변 woff2(1.3MB, v1.0.3)를 저장소에 넣고 `next/font/local`로 불러온다. 대회장 네트워크와 무관하게 동작하게 하기 위함이다. Geist Mono는 `next/font/google`로 불러온다. 정적 HTML 목업에서는 jsDelivr의 split CSS를 쓴다.
- **폴백:** `"Pretendard Variable", "Apple SD Gothic Neo", sans-serif`
- **규칙:** Geist Mono는 숫자에만 쓴다. 한글이 섞인 줄에 쓰면 자간이 벌어진다. 한글이 섞인 숫자 줄은 Wanted Sans + `tabular-nums`로 처리한다.
- **줄바꿈:** 전역에 `word-break: keep-all`을 적용해 한글 단어 중간에서 끊기지 않게 한다.

| 단계 | 크기 / 행간 | 굵기 | 자간 |
|---|---|---|---|
| Hero | 64 / 1.08 | 750 | −4% |
| Display (판정 헤드라인) | 44 / 1.15 | 750 | −3.5% |
| H1 (화면 제목) | 24 / 1.3 | 700 | −2.5% |
| H2 | 20 / 1.35 | 650 | −2% |
| Body | 16 / 1.65 | 400 | 0 |
| Small | 14 / 1.55 | 400 | 0 |
| Label | 13 / 1.4 | 550 | 0 |
| Price (판정 금액) | 56–64 / 1.0 | Geist Mono 600 | −4% |

## 색

- **방식:** 절제형. 브랜드 색은 따로 두지 않는다. 주요 버튼은 먹색이다.

| 토큰 | 라이트 | 다크 | 용도 |
|---|---|---|---|
| `bg` | `#F2F0EA` | `#12110D` | 재생지 바탕 |
| `surface` | `#FBFAF6` | `#1B1A15` | 패널, 표 |
| `sunken` | `#E9E6DE` | `#0D0C09` | 들어간 면, 세그먼트 바탕 |
| `line` | `#DEDBD2` | `#2E2C25` | 구분선 |
| `line-strong` | `#C9C5BA` | `#3E3B32` | 입력 테두리 |
| `ink` | `#16150F` | `#F1EFE8` | 글씨, 주요 버튼 바탕 |
| `ink-2` | `#3A3830` | `#D2CFC5` | 본문 |
| `muted` | `#6B675E` | `#A39F94` | 보조 글씨 (4.9:1 / 7.2:1) |
| `marker` | `#E6FF3D` | `#E6FF3D` | AI 표시 전용 |
| `gain` | `#0C7148` | `#43C98A` | 이익 (+) |
| `gain-bg` | `#E1F1E6` | `#12291E` | 이익 안내 바탕 |
| `loss` | `#B5332A` | `#FF7266` | 손실 (−), 막힌 조건 |
| `loss-bg` | `#F8E4DF` | `#2D1714` | 손실 안내 바탕 |
| `warn` | `#9A5B00` | `#E0A23A` | 확인 필요, 정보 부족 |
| `warn-bg` | `#F6ECD8` | `#2A2112` | |
| `photo` | `#2B2A24` | `#0B0A08` | 사진 영역 바탕 |

### 색 규칙

1. **형광펜은 AI가 표시한 것에만 쓴다.** 바운딩박스, 인용 조항·핵심 수치 밑줄, 현재 단계 번호, 추천 행 배경이 여기에 해당한다. 버튼에는 쓰지 않는다.
2. **색만으로 의미를 전달하지 않는다.** 손익은 항상 `+`/`−`(U+2212) 부호와 "수익·지출" 라벨을 함께 쓴다.
3. **초록은 이익 숫자에만 쓴다.** 초록이 보이는 순간 자체가 의미를 갖도록 한다.
4. **한 화면에 먹색 버튼은 하나만 둔다.** 나머지 행동은 테두리 버튼이나 텍스트 버튼으로 낮춘다.
5. **차트 색:** 이익 막대는 `gain`, 손실 막대는 `loss`, 중립 계열은 `ink-2`와 `muted`를 쓴다.

## 간격

- **기본 단위:** 4px
- **밀도:** 표와 근거 기록은 촘촘하게, 판정 영역은 넓게 둔다.
- **척도:** 2xs(2) xs(4) sm(8) md(16) lg(24) xl(32) 2xl(48) 3xl(64) 4xl(88)

## 레이아웃

- **방식:** 12열 그리드를 엄격하게 지킨다.
- **앱 틀:** 좌측 단계 메뉴 208px + 본문. 본문 안쪽 여백은 28px / 32px이다.
- **판정·식별 화면:** 사진 7열, 판정 5열로 나눈다.
- **최대 너비:** 1200px (문서형 화면), 앱은 화면 폭을 채운다.
- **거터:** 24px
- **모서리:** sm 4 (태그), md 6 (버튼·입력), lg 10 (패널), 앱 틀 14, full (배지·칩)
- **사진:** 사용자가 찍은 사진을 보정 없이 크게 쓴다. 바운딩박스는 형광펜 1.5px 테두리, 이물질은 2px 테두리와 14% 형광펜 채움, 라벨은 형광펜 바탕에 Geist Mono 11px로 쓴다.
- **단계 간 맥락:** 제목 아래 "지금까지 확정" 칩 띠를 단계마다 누적한다 (v2 감사 결과 유지).

## 모션

- **방식:** 기능적 전환만 쓴다. 예외는 시그니처 모션 하나다.
- **이징:** 들어올 때 `cubic-bezier(.2,.7,.2,1)`, 이동할 때 `cubic-bezier(.6,0,.3,1)`
- **시간:** 호버·포커스 180ms, 패널·테마 전환 300ms
- **시그니처 "테이프 떼기":** 판정 카드가 처음 보일 때 한 번 재생한다. 테이프 바운딩박스가 스티커처럼 떨어지고(700ms), 금액이 −250에서 +300으로 올라간다(1100ms, ease-out cubic, 10원 단위). 0을 넘는 순간 색이 `loss`에서 `gain`으로 바뀌고 패널 바탕이 `gain-bg`로 잠깐 번진다. 박스나 "다시 보기"를 누르면 다시 재생한다.
- **모션 감소:** `prefers-reduced-motion`이면 모든 전환을 끄고 결과값만 보여 준다.

## 컴포넌트 규칙

- **버튼:** 최소 높이 44px. primary(먹), secondary(테두리), ghost(텍스트) 세 종류만 쓴다.
- **포커스:** 먹색 2px 외곽선 + 형광펜 5px 링을 쓴다.
- **배지:** 재활용 가능(gain), 매입 거절(loss), 확인 필요(warn), AI 판정(marker), 초안(neutral)
- **판정 3단계 배지:** 새 색을 만들지 않고 채움 강도로 구분한다. 재사용 가능은 `gain` 꽉 채움에 흰 글씨, 재활용 가능은 `gain-bg` 바탕에 `gain` 글씨, 폐기 처리는 `loss-bg` 바탕에 `loss` 글씨를 쓴다.
- **에이전트 근거 기록:** 시각 · 에이전트 · 판단 문장 · 출처 · 신뢰도 순서의 행으로 표시한다. 채팅 말풍선으로 표시하지 않는다.
- **규정 체크리스트:** 영수증 형식. 항목 · 점선 리더 · 결론, 그 아래에 「법령명」 제○조를 인용한다. 정보가 부족한 항목은 형광펜 `?` 아이콘과 되묻기 상자를 쓴다.
- **비교표:** 금액은 오른쪽 정렬, 단위는 열 제목에 둔다. 추천 행은 왼쪽 먹색 3px 막대와 13% 형광펜 바탕으로 표시한다. 표 아래에 계산 가정을 명시한다.
- **승인 게이트:** 외부 발송 버튼은 먹색 1px 테두리 상자 안에 두고, 발송 대상과 확인 항목을 체크박스로 나열한다.

## Tailwind 4 토큰 (frontend `src/app/globals.css`)

아래는 요약이다. 실제 구현은 frontend 저장소의 `src/app/globals.css`이며, 그쪽에서는 `--color-*: initial`로 Tailwind 기본 팔레트를 끄고 글자 크기 토큰(`text-display`, `text-h1`, `text-h2`, `text-label`)과 숫자 전용 `num` 유틸리티를 추가로 정의한다.

```css
@import "tailwindcss";

@theme {
  --color-bg: #F2F0EA;
  --color-surface: #FBFAF6;
  --color-sunken: #E9E6DE;
  --color-line: #DEDBD2;
  --color-line-strong: #C9C5BA;
  --color-ink: #16150F;
  --color-ink-2: #3A3830;
  --color-muted: #6B675E;
  --color-marker: #E6FF3D;
  --color-gain: #0C7148;
  --color-gain-bg: #E1F1E6;
  --color-loss: #B5332A;
  --color-loss-bg: #F8E4DF;
  --color-warn: #9A5B00;
  --color-warn-bg: #F6ECD8;
  --color-photo: #2B2A24;

  --font-sans: "Wanted Sans Variable", "Pretendard Variable", "Apple SD Gothic Neo", sans-serif;
  --font-mono: var(--font-geist-mono), ui-monospace, monospace;

  --radius-sm: 4px;
  --radius-md: 6px;
  --radius-lg: 10px;

  --ease-out: cubic-bezier(.2,.7,.2,1);
  --ease-in-out: cubic-bezier(.6,0,.3,1);
}

@custom-variant dark (&:where([data-theme="dark"], [data-theme="dark"] *));

[data-theme="dark"] {
  --color-bg: #12110D;
  --color-surface: #1B1A15;
  --color-sunken: #0D0C09;
  --color-line: #2E2C25;
  --color-line-strong: #3E3B32;
  --color-ink: #F1EFE8;
  --color-ink-2: #D2CFC5;
  --color-muted: #A39F94;
  --color-gain: #43C98A;
  --color-gain-bg: #12291E;
  --color-loss: #FF7266;
  --color-loss-bg: #2D1714;
  --color-warn: #E0A23A;
  --color-warn-bg: #2A2112;
  --color-photo: #0B0A08;
}

body {
  background: var(--color-bg);
  color: var(--color-ink);
  font-family: var(--font-sans);
  word-break: keep-all;
  overflow-wrap: break-word;
}
```

## 결정 기록

| 날짜 | 결정 | 근거 |
|---|---|---|
| 2026-11-09 | 디자인 시스템 v1 수립 (산업 원장) | `/design-consultation`. 경쟁 서비스 조사와 Codex·Claude 서브에이전트 외부 의견을 종합했다 |
| 2026-11-09 | 기억시킬 한 가지를 "쓰레기가 돈이 된다"로 정함 | 사용자 선택. 손익 전환이 모든 화면의 중심이 된다 |
| 2026-11-09 | 손익 색은 초록(+) / 빨강(−) | 사용자 선택. 처리비 지출은 '적자'라는 회계 감각과 맞는다. 증시식(빨강+)은 검토 후 제외했다 |
| 2026-11-09 | 판정 헤드라인은 Wanted Sans 굵게 | 사용자 선택. 서체 하나로 통일한다. 한글 세리프(Hahmlet)는 검토 후 제외했다 |
| 2026-11-09 | 초록 브랜드 색과 자연 이미지 배제 | 폐기물·ESG 제품과 구별하기 위함. 세 의견이 모두 일치했다 |
| 2026-11-09 | 형광펜 `#E6FF3D`를 AI 표시 전용으로 사용 | 노란색이 보이면 곧 AI 근거라는 뜻이 되도록 의미를 하나로 고정한다 |
