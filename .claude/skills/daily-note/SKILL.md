---
name: daily-note
description: Use when the user says "데일리 노트 생성" — creates today's daily note in the dev-wiki vault, carries over unfinished items (오늘 할 일·팔로업) from the previous note, inserts today's Google Calendar events, and adds today's hot dev issues from web search
---

# 데일리 노트 생성

## 개요

"데일리 노트 생성" 호출 시 아래 5단계를 순서대로 실행한다.

## 절차

### Step 1 — 파일 존재 확인

- 오늘 날짜(`currentDate` 컨텍스트 또는 `date` 명령으로 확인)와 요일을 구한다.
- `/Users/woohyungrae/Desktop/dev-wiki/데일리/YYYY-MM-DD.md` 파일이 이미 있으면 **"이미 존재합니다"** 라고 알리고 파일 경로를 보여준 뒤 종료한다.
- 없으면 Step 2로 진행한다.

### Step 2 — 데일리 노트 생성

아래 템플릿으로 파일을 생성한다.
**frontmatter(속성 영역)와 H1 제목 없이** 첫 줄부터 섹션을 시작하고, 섹션 사이 빈 줄을 두지 않는다. 날짜는 파일명(`YYYY-MM-DD.md`)으로 식별한다.

```markdown
## 오늘 일정
## 오늘 할 일
- [ ] 
## 팔로업
## 오늘의 개발 이슈
```

별도 `## 메모` 섹션은 두지 않는다. 메모성 항목도 `## 팔로업`에 기록한다.

### Step 3 — 이전 노트에서 미완료 항목 이월

- `데일리/` 폴더에서 가장 최근 데일리 노트 파일을 찾는다 (오늘 날짜 제외).
  - 파일이 없으면 이 단계를 건너뛴다.
- 이전 노트의 **`## 오늘 할 일`, `## 팔로업`** 두 섹션을 각각 읽어, **완료·취소되지 않은 항목만** 새 노트의 같은 섹션으로 그대로 복사한다.
  - 이전 노트에 `## 메모` 섹션이 남아 있으면(구 형식), 그 미완료 항목은 `## 팔로업`으로 이월한다.
  - **제외**: `- [x]`(완료), `- [-]`(취소) 항목.
  - **제외**: 내용 없는 빈 placeholder (`- [ ]` 뒤에 텍스트 없음).
  - 그 외 항목(`- [ ]` 미완료, `- [/]` 진행중, `- [!]` 중요, `- [?]` 확인필요, `- [*]`, `- [i]` 등)은 아이콘을 원본 그대로 유지해 이월한다.
  - 출처 날짜를 뒤에 추가하지 않는다 (원본 텍스트 그대로).
- `## 오늘 일정`과 `## 오늘의 개발 이슈`는 이월하지 않는다 (매일 새로 채운다).
- 이월 결과 `## 오늘 할 일`이 비면 빈 `- [ ] ` 한 줄을 남긴다.

### Step 4 — Google Calendar 일정 추가

- `mcp__claude_ai_Google_Calendar__list_events`를 호출해 오늘 날짜 이벤트를 가져온다.
  - startTime: `YYYY-MM-DDT00:00:00`, endTime: `YYYY-MM-DDT23:59:59`, timeZone: `Asia/Seoul`, orderBy: `startTime`
  - 사용자 캘린더(`rea1109@squares.ai`)와 스퀘어스 공유 캘린더(`sqs@squares.ai`) 모두 조회한다.
- `rea1109@squares.ai`가 attendees에 포함된 이벤트만 `## 오늘 일정` 섹션에 시간순으로 삽입한다.
  - 형식: `- [<] HH:MM 이벤트명` (Minimal 테마 Schedule 아이콘)
  - 종일 이벤트: `- [<] (종일) 이벤트명`
- 인증 안 됨, 연결 불가, 일정 없음의 경우 섹션을 빈 채로 두고 계속 진행한다.

### Step 5 — 오늘의 개발 이슈 추가

- WebSearch로 당일 화제가 된 개발 이슈를 검색한다.
  - 검색 쿼리 예: `"AI news today YYYY-MM-DD"`, `"AI coding tools news"`, `"frontend developer news"` 등 2~3회 검색해 결과를 모은다.
- 선정 기준: **AI 관련 이슈(모델 릴리스, AI 코딩 도구, AI 업계 동향) 위주**, 프론트엔드(React, TypeScript, 브라우저, JS 생태계) 이슈도 포함. 총 **3~5개**.
- `## 오늘의 개발 이슈` 섹션에 삽입한다.
  - 형식: `- [I] [제목](링크) — 한 줄 요약` (Minimal 테마 Info 아이콘)
  - 제목은 한국어로 요약하되, 기술 용어는 원문 유지.

```markdown
## 오늘의 개발 이슈
- [I] [Claude Opus 4.8 출시](https://...) — SWE-bench Verified 88.6%, 1M 토큰 기본 컨텍스트
- [I] [React 19.2 릴리스 — Activity 컴포넌트 추가](https://react.dev/...) — Suspense 경계 외부에서 UI 상태 보존 가능
```

- 검색 실패 또는 유의미한 이슈가 없으면 섹션을 빈 채로 두고 계속 진행한다.

## 완료 후

파일 경로를 사용자에게 알리고, 이월 항목 수(할 일·팔로업)·캘린더 일정 수·개발 이슈 수를 한 줄로 요약한다.
예: `데일리/2026-06-11.md 생성 완료 — 이월 5개, 일정 2개, 개발 이슈 4개`
