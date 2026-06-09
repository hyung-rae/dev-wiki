---
tags:
  - troubleshooting
  - docker
  - dns
  - network
created: 2026-06-09
status: resolved
---

# Docker 컨테이너 내부 DNS 해석 간헐적 실패

## 증상 / 문제
배포 후 애플리케이션 컨테이너에서 외부 API 호출이 간헐적으로 실패.
로그에 다음 에러가 불규칙하게 발생했다.

```
Error: getaddrinfo EAI_AGAIN api.external-service.com
```

- 재현 조건: 트래픽이 몰리는 시간대에 빈도 증가, 평소엔 잘 됨
- 컨테이너 재시작하면 잠깐 괜찮아졌다가 다시 발생

## 환경
- 스택/버전: Docker 24.0, docker-compose, Node.js 20 (alpine 이미지)
- 발생 위치: 운영 서버 (Ubuntu 22.04), bridge 네트워크 사용

## 원인
호스트의 `systemd-resolved`가 제공하는 DNS 캐시(127.0.0.53)와
Docker 기본 embedded DNS(127.0.0.11) 사이에서 동시 요청이 몰릴 때
일부 쿼리가 타임아웃되어 `EAI_AGAIN`(일시적 실패)으로 떨어졌다.

근본 원인은 **alpine(musl libc)의 DNS resolver가 UDP 응답을 한 번만 시도하고
재시도 동작이 glibc보다 공격적이지 않은 점** + DNS 응답 지연이 겹친 것.

## 해결 방법
1. compose에 명시적 DNS 서버를 지정해 캐시 의존도를 낮춤.
   ```yaml
   services:
     app:
       dns:
         - 8.8.8.8
         - 1.1.1.1
   ```
2. resolver 재시도/타임아웃을 늘려 일시적 실패에 견디도록 설정.
   ```
   # /etc/resolv.conf (또는 컨테이너 빌드 시 주입)
   options timeout:2 attempts:3
   ```
3. 재배포 후 부하 테스트(`vegeta` 동시 요청)로 `EAI_AGAIN` 미재현 확인.

## 배운 점 / 재발 방지
- alpine 이미지의 musl resolver는 DNS 실패에 취약 → DNS 민감한 서비스는 `dns`/`options` 명시 또는 debian-slim 이미지 고려.
- `EAI_AGAIN`은 "DNS가 죽음"이 아니라 **"일시적 실패"** 라는 신호 → 네트워크/캐시/타임아웃부터 의심.
- 모니터링에 DNS 해석 실패 카운트 메트릭 추가해 조기 감지.

## 참고 자료
- [musl libc DNS resolver 한계 논의](https://wiki.musl-libc.org/functional-differences-from-glibc.html)
- [[2026-06-09]]
