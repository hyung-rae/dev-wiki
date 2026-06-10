---
tags:
  - claude-code
  - permissions
---
`~/.claude/settings.json`(글로벌) 또는 `.claude/settings.json`(프로젝트)의 `permissions` 블록으로 툴 자동 승인/거부를 제어한다.

## settings.json 구조

```json
{
  "permissions": {
    "allow": [
      "Read",
      "Bash(grep *)",
      "Bash(git *)",
      "mcp__github__get_issue"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(git push --force *)",
      "Bash(git reset --hard *)"
    ]
  }
}
```

- `allow` — 목록에 있는 툴은 프롬프트 없이 자동 실행
- `deny` — 목록에 있는 툴은 **어떤 옵션을 써도 무조건 차단**

> [!warning] deny 우선순위
> `deny > --dangerously-skip-permissions > allow`
> `--dangerously-skip-permissions` 플래그로도 deny는 override되지 않는다.

## 시작 옵션

| 옵션 | 설명 |
|------|------|
| `--dangerously-skip-permissions` | 모든 권한 프롬프트 스킵 (deny는 여전히 차단) |
| `--model claude-sonnet-4-6` | 사용할 모델 지정 |
| `--print "질문"` | 비대화형 — 바로 출력 후 종료 |
| `--allowedTools "Read,Edit"` | 세션 내 허용 툴 지정 |
| `--max-turns 10` | 최대 대화 턴 수 제한 |
| `--mcp-config path.json` | MCP 설정 파일 지정 |

## 권장 deny 목록 (위험 커맨드)

```json
"deny": [
  "Bash(rm -rf *)",
  "Bash(git push --force *)",
  "Bash(git push -f *)",
  "Bash(git reset --hard *)",
  "Bash(git clean -f *)",
  "Bash(chmod 777 *)",
  "Bash(sudo rm *)",
  "Bash(dd *)",
  "Bash(mkfs *)"
]
```

## 설정 팁

- 프롬프트가 뜰 때 **"Always allow"** 선택 → 해당 패턴이 자동으로 settings.json에 추가됨
- `/permissions` 커맨드로 현재 등록된 목록 확인 가능
- ==안전한 전체 허용 패턴==: `--dangerously-skip-permissions` + `deny`에 위험 커맨드 등록

