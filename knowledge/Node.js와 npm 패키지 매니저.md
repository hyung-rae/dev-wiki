---
tags:
  - dependency-management
  - npm
  - yarn
  - nodejs
---
==Node.js는 JavaScript를 웹 브라우저가 아닌 환경에서도 실행할 수 있게 해주는 런타임==이다. 브라우저 밖으로 나오면서 **코드를 공유할 저장소**가 필요해졌고, 그 역할을 npm이 맡는다.

| 언어 | 패키지 저장소 |
| --- | --- |
| Java | Maven |
| Python | PyPI |
| **Node.js** | **npm** (node package manager, npmjs.com) |

## npm과 yarn
Node.js를 설치하면 npm이 함께 깔린다. **yarn은 Facebook이 npm의 속도를 보완하려고 만든 대안 패키지 매니저**로, npm으로 설치해서 쓴다.

```shell
npm install -g yarn   # -g : 전역 설치
```

두 도구는 같은 npm 레지스트리를 바라보므로 설치되는 패키지는 동일하다. 다른 것은 **의존성 해석 방식과 락 파일**(`package-lock.json` vs `yarn.lock`)이다.

> [!warning]
> 한 프로젝트에서 **npm과 yarn을 섞어 쓰면 락 파일이 두 개 생겨** 팀원마다 다른 버전이 설치될 수 있다. 하나로 통일해야 한다.

## 관련 노트
- [[Next.js 프로젝트 초기 구조]] — 패키지 매니저가 만들어내는 파일들
- [[node_modules 호이스팅]] — 설치된 패키지가 실제로 놓이는 구조
- [[의존성 관리]]
