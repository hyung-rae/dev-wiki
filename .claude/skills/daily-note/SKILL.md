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
  - **제외**: `- [x]`(완료), `- [-]`(취소) 항목 — 이 둘만 이월에서 빠진다.
  - **제외**: 내용 없는 빈 placeholder (`- [ ]` 뒤에 텍스트 없음).
  - 그 외 항목(`- [ ]` 미완료, `- [/]` 진행중, `- [!]` 중요, `- [?]` 확인필요, `- [*]`, `- [i]` 등)은 아이콘을 원본 그대로 유지해 이월한다.
  - **`- [/]` 진행중 항목은 완료(`[x]`)·취소(`[-]`)로 바뀌기 전까지 매일 이어서 이월한다** (중간에 끊기지 않도록 주의).
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

- **출처 우선순위**대로 채운다. 총 **3~5개**.
  1. **GeekNews** (`https://news.hada.io/`) — WebFetch로 인기 글 목록을 가져온다. 각 글의 상세 링크는 `https://news.hada.io/topic?id=...` 형태.
  2. **요즘IT** (`https://yozm.wishket.com/magazine/`) — WebFetch로 최신 매거진 글을 가져온다. 상세 링크는 `https://yozm.wishket.com/magazine/detail/숫자/` 형태.
  3. **추천 보충** — 위 두 곳에서 3개를 못 채우거나 그날 굵직한 AI/프론트엔드 소식이 따로 있으면 WebSearch로 보충한다.
  - 위 1·2를 우선 채우고, 모자란 만큼만 3에서 보충한다 (예: GeekNews 3 + 요즘IT 2).
- 선정 기준: **AI 관련 이슈(모델 릴리스, AI 코딩 도구, AI 업계 동향) 위주**, 프론트엔드(React, TypeScript, 브라우저, JS 생태계) 이슈도 포함.
- `## 오늘의 개발 이슈` 섹션에 삽입한다.
  - 형식: `- [I] [제목](링크) — 한 줄 요약 (출처)` (Minimal 테마 Info 아이콘)
  - 제목은 한국어로 요약하되, 기술 용어는 원문 유지. 출처는 `(GeekNews)` / `(요즘IT)`로 표기하고, 추천 보충 항목은 출처를 생략한다.

```markdown
## 오늘의 개발 이슈
- [I] [Cate — 무한 줌이 가능한 코딩용 캔버스 IDE](https://news.hada.io/topic?id=30438) — 무한 캔버스 위 공간형 레이아웃으로 개발 도구를 통합 (GeekNews)
- [I] [정말로 지금은 Codex가 Claude Code보다 나을까?](https://yozm.wishket.com/magazine/detail/3771/) — 두 AI 코딩 도구의 성능·특징 비교 (요즘IT)
```

- 검색 실패 또는 유의미한 이슈가 없으면 섹션을 빈 채로 두고 계속 진행한다.

## 완료 후

파일 경로를 사용자에게 알리고, 이월 항목 수(할 일·팔로업)·캘린더 일정 수·개발 이슈 수를 한 줄로 요약한다.
예: `데일리/2026-06-11.md 생성 완료 — 이월 5개, 일정 2개, 개발 이슈 4개`
