---
name: edu-landing-page
description: |
  교육 과정(강의, 부트캠프, 워크숍, 캠프 등)의 랜딩 페이지를 완성도 높은 단일 HTML 파일로 만드는 스킬.
  다음 상황에서 반드시 이 스킬을 사용할 것:
  - "HTML로 만들어줘", "랜딩 페이지 만들어줘", "과정 소개 페이지 만들어줘" 등 교육 과정 관련 웹 페이지 요청
  - 커리큘럼, 강사 소개, 대상자, FAQ, CTA 등의 섹션이 포함된 교육 콘텐츠가 있을 때
  - 기획된 교육 과정 내용을 정리된 웹 페이지 형태로 출력해야 할 때
  - 특정 기업/브랜드의 디자인 가이드에 맞춰 교육 과정 페이지를 제작해야 할 때
  단순 코드 스니펫이나 컴포넌트 요청이 아닌, 실제 다운로드/배포 가능한 완성형 HTML 페이지를 원할 때 사용.
---

# 교육 과정 랜딩 페이지 제작 스킬

재직자 업스킬, 부트캠프, 워크숍 등 교육 과정의 완성형 HTML 랜딩 페이지를 제작한다.
단일 HTML 파일로 출력하며, 외부 프레임워크 없이 순수 HTML/CSS/JS로 구현한다.

---

## Step 0: 브랜드/디자인 가이드 파악

페이지 제작 전 반드시 디자인 방향을 확정한다.

**사용자가 브랜드 가이드를 제시한 경우**
→ 해당 가이드의 컬러, 서체, 레이아웃 원칙을 최우선으로 따른다.

**브랜드 가이드가 없는 경우**
→ `/mnt/skills/public/frontend-design/SKILL.md`를 읽고 독창적인 디자인 방향을 결정한다.
→ 다크/라이트 테마, 서체 조합, 강조 색상을 명시적으로 선택한 후 구현한다.

**Grepp/프로그래머스 브랜드 가이드 (자주 쓰이는 케이스)**
→ 아래 `## Grepp 디자인 시스템` 섹션을 참고한다.

---

## Step 1: 콘텐츠 구조 파악

대화 맥락에서 다음 항목을 추출한다. 없는 항목은 합리적으로 채운다.

| 항목 | 설명 |
|------|------|
| 과정명 | 정식 명칭 + 영문 서브타이틀 |
| 핵심 페인포인트 | 타겟이 느끼는 문제 3~4개 |
| 과정 개요 | 시간, 형태(오프라인/온라인), 정원, 장소 |
| 커리큘럼 | Phase/Sprint 단위 세부 일정 + 각 결과물 |
| 강사 정보 | 이름, 역할, 한 줄 철학/인용구, 커리어 |
| 대상자 | 환영하는 분 / 맞지 않는 분 (양쪽 모두) |
| 수료 후 결과물 | 숫자로 표현 가능한 구체적 아웃컴 |
| 운영 정보 | 일시, 장소, 비용, 포함 사항 |
| FAQ | 자주 묻는 질문 5개 내외 |

---

## Step 2: 페이지 섹션 구성

아래 섹션 순서를 기본으로 한다. 콘텐츠 상황에 따라 섹션을 추가/생략할 수 있다.

```
1.  GNB (고정 상단 네비게이션)
2.  Hero (과정명 + 핵심 메시지 + CTA)
3.  Stats Band (숫자로 보는 핵심 지표 4개)
4.  Pain Section (타겟의 페인포인트)
5.  Before / After (과정 전후 비교)
6.  Curriculum (탭 or 타임라인 형식 상세 커리큘럼)
7.  Instructor (강사 소개)
8.  Target (대상자 / 비대상자)
9.  Outcomes (수료 후 결과물)
10. Logistics (일정·장소·비용·포함사항)
11. FAQ (아코디언)
12. CTA Section (최종 신청 유도)
13. Footer
```

**후킹 요소 체크리스트** — 아래 항목이 페이지에 반드시 포함되어야 한다:
- [ ] Hero 헤드라인: 타겟의 페인포인트를 직접 질문/도발하는 문장
- [ ] BEFORE/AFTER: 추상적 혜택이 아닌 구체적 상황 대비
- [ ] 커리큘럼 각 세션: 세션 종료 후 손에 남는 결과물 명시
- [ ] 대상자 필터: 환영하는 분 + 맞지 않는 분 양쪽 모두
- [ ] Stats Band: 숫자로 표현된 임팩트 4개
- [ ] 강사 인용구: 과정 철학을 담은 직접 인용 형식

---

## Step 3: HTML 구현 규칙

### 파일 구조
- 단일 `.html` 파일에 CSS, JS 모두 인라인
- Google Fonts는 `<link>` 태그로 외부 로드 허용
- 외부 JS 라이브러리는 사용하지 않음 (순수 Vanilla JS)

### 인터랙션 (필수 구현)
- **커리큘럼 탭**: 좌측 nav 클릭 시 우측 패널 전환 (JS)
- **FAQ 아코디언**: 클릭 시 펼침/접힘 (JS, max-height transition)
- **스크롤 페이드인**: IntersectionObserver로 섹션 진입 시 fadeUp 애니메이션
- **GNB**: sticky, 스크롤 시 배경 blur 처리

### 반응형
- 브레이크포인트: 900px (태블릿), 600px (모바일)
- 그리드: 데스크탑 다단 → 모바일 1단으로 자동 전환
- 폰트 크기: `clamp()` 함수로 뷰포트 대응

### 성능
- 애니메이션은 CSS `transform`, `opacity`만 사용 (레이아웃 리플로우 방지)
- 이미지 없이 CSS만으로 시각적 완성도 확보

---

## Grepp 디자인 시스템

Grepp(프로그래머스) 브랜드 가이드 기반 과정 페이지를 만들 때 적용한다.

### 컬러 토큰
```css
:root {
  --deep: #202A2F;          /* 메인 브랜드 컬러 (딥 네이비) */
  --deep-12: rgba(32,42,47,0.08);
  --accent: #00B493;        /* 포인트 컬러 (청록) */
  --accent-dim: rgba(0,180,147,0.10);
  --accent-border: rgba(0,180,147,0.28);
  --red: #E84057;           /* 경고/강조 (페인포인트 아이콘 등) */
  --red-dim: rgba(232,64,87,0.08);
  --text-primary: #1a2126;
  --text-secondary: #4a5560;
  --text-muted: #8a9aa5;
  --border: #e4e8eb;
  --border-strong: #c8d0d6;
  --surface: #f5f7f8;       /* 섹션 배경 교체용 */
  --surface2: #eef1f3;
  --white: #ffffff;
}
```

### 서체 조합
```html
<!-- Google Fonts 로드 -->
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```
- **한글 본문**: `Noto Sans KR` — 300/400/500/700
- **영문/숫자**: `Inter` — 400/500/600/700
- **코드/모노**: `JetBrains Mono` — 코드 블록, 태그, 시간 표기, 기술적 레이블에 사용
- **금지**: Arial, Roboto, system-ui 등 제네릭 폰트

### 레이아웃 원칙
- 기본 배경: `#ffffff` (화이트)
- 섹션 구분: `--surface(#f5f7f8)` 교체 — 색상이 아닌 명도로만 구분
- 다크 섹션: `--deep(#202A2F)` — Hero, CTA, 강사 카드 좌측 패널 등 포인트 구간에만 사용
- 불필요한 색상 추가 엄금 — `--accent` 외 추가 컬러 사용 최소화
- 테두리: `1px solid var(--border)` 기본, 강조 시 `--border-strong`

### Grepp 전용 UI 패턴

**코드 블록 장식 (개발자 친화적 연출)**
```html
<div class="code-block">
  <div class="code-block__bar">
    <span class="code-dot" style="background:#ff5f57"></span>
    <span class="code-dot" style="background:#febc2e"></span>
    <span class="code-dot" style="background:#28c840"></span>
    <span class="code-block__label">schedule.json</span>
  </div>
  <div class="code-block__body" style="font-family: var(--mono);">
    <!-- 커리큘럼 타임라인을 JSON 형식으로 표현 -->
  </div>
</div>
```

**모노스페이스 레이블** — 시간, 태그, eyebrow에 적용
```css
.eyebrow { font-family: var(--mono); font-size: 11px; letter-spacing: 0.12em; text-transform: uppercase; color: var(--accent); }
.time-badge { font-family: var(--mono); font-size: 12px; }
```

**GNB 구조**
```
[로고마크] [Grepp 교육개발] | [과정명]          [수강 신청하기 버튼]
```

### 섹션별 배경 교체 패턴 (Grepp)
```
Hero:        --deep 배경 + 그리드 오버레이 + 미묘한 accent 방사형 gradient
Stats Band:  --surface 배경
Pain:        --white 배경
Before/After: --surface 배경
Curriculum:  --white 배경
Instructor:  --surface 배경 (카드 좌측은 --deep)
Target:      --white 배경
Outcomes:    --deep 배경
Logistics:   --white 배경
FAQ:         --surface 배경
CTA:         --deep 배경 + 하단 accent 방사형 gradient
Footer:      #0e1118 배경
```

---

## Step 4: 출력 및 전달

1. `/home/claude/[과정명-slug].html` 에 파일 생성
2. `/mnt/user-data/outputs/[과정명-slug].html` 에 복사
3. `present_files` 도구로 사용자에게 전달
4. 전달 후 한 줄 요약: 구현된 주요 섹션 수 + 인터랙션 항목 언급

---

## 참고: 후킹 요소 작성 가이드

페이지의 전환율을 높이는 카피라이팅 패턴.

**Hero 헤드라인 공식**
```
[타겟이 매일 겪는 불만 상황]을 직접 질문으로 던진다.
예: "아이디어를 검증하는 데 왜 3개월이 걸려야 하나요?"
예: "개발팀에 요청서를 넣고 얼마나 더 기다리실 건가요?"
```

**Pain 카드 공식**
```
실제 직군/연차 페르소나의 말투로 작성
예: "이 가설이 맞는지 확인만 하면 되는데, 개발팀 일정이 3달 뒤야."
     // 신사업팀 팀장, 3년차
```

**커리큘럼 결과물 명시 공식**
```
각 세션 끝에 반드시 포함:
"결과물: [구체적이고 손에 잡히는 산출물]"
예: "결과물: 실제 배포 URL — 지금 바로 공유 가능한 나의 첫 서비스"
```

**대상자 필터 공식**
```
환영하는 분: 구체적 상황/역할로 공감 유발 → "이건 나를 위한 과정"
맞지 않는 분: 과감하게 거절 → 진지한 참가자만 선별 + 희소성 연출
```
