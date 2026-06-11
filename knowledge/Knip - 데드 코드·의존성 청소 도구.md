---
tags:
  - knip
  - dead-code
  - dependency-management
  - tree-shaking
---
**Knip**(네덜란드어 "자르다")은 JS/TS 프로젝트의 ==데드 코드·미사용 의존성==을 찾아내는 청소 도구다. 핵심: **진입점부터 프로젝트 전체 모듈 그래프를 추적**해, 단일 파일 검사로는 못 잡는 미사용 파일·`export`·패키지를 잡아낸다.

## ESLint와의 차이
| | 검사 범위 | 잡는 것 |
| --- | --- | --- |
| **ESLint** (`no-unused-vars`) | **단일 파일 내부** | 파일 안에서 선언 후 안 쓴 변수 |
| **Knip** | **프로젝트 전체 그래프** | 미사용 파일 자체, 아무도 `import` 안 하는 `export` |

> [!info] ESLint는 파일 안에서 `export`된 코드가 프로젝트 전체에서 방치 중인지는 모른다. Knip은 그 빈틈을 메운다.

## 찾아내는 6가지
1. **Unused Files** — 어디서도 import하지 않는 고립 파일
2. **Unused Dependencies** — 설치됐으나 코드에서 안 쓰는 패키지
3. **Unused DevDependencies** — 빌드·린트·테스트에 안 쓰는 개발 패키지
4. **Unused Exports** — `export` 했으나 아무도 `import` 안 하는 함수/타입/변수
5. **Unlisted Dependencies** — 코드에선 쓰는데 `package.json`에 없는 패키지
6. **Unresolved Imports** — 잘못된 경로·없는 파일을 가리키는 깨진 import

## 주요 명령어
```bash
pnpm add -D knip typescript @types/node   # 설치
npx knip            # 검사
npx knip --fix      # 미사용 export·의존성 자동 제거
```

## CI 도입
미사용 코드·누락 패키지가 메인 브랜치로 새는 걸 빌드 전에 막으려면 CI에 추가한다. GitHub Actions라면 `pull_request` 트리거로 `pnpm knip` 스텝을 둔다.

> [!tip] 도입 초기엔 데드 코드가 많아 CI가 계속 깨지므로 `--no-exit-code`로 **경고만 출력**하는 적응 기간을 둔다. 이후 `--dependencies --files`처럼 대상을 좁혀 점진적으로 엄격화한다.

- 동적 로딩 등으로 오탐하는 코드는 `// @knipignore` 주석으로 예외 처리.

## 관련 노트
- [[JS·TS 미사용 패키지 정리 도구 비교]] — depcheck·npm-check와의 비교, Knip이 상위 호환인 이유
