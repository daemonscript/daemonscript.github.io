# DaeMonScript Gaming 계정 시스템

## 운영 구성
- Frontend: GitHub Pages `https://daemonscript.github.io`
- API: Cloudflare Worker `https://daemonscript-gaming-auth.youthdeveloper-github.workers.dev`
- Database: Cloudflare D1 `daemonscript-gaming-auth` (APAC)
- Worker binding: `DB` → D1 database
- CORS 허용 Origin: `https://daemonscript.github.io`

## 구현된 API
| Method | Endpoint | 기능 |
|---|---|---|
| POST | /api/auth/register | 이메일·비밀번호·닉네임 회원가입 및 세션 발급 |
| POST | /api/auth/login | 로그인 및 세션 발급 |
| POST | /api/auth/logout | 현재 세션 폐기 |
| GET | /api/auth/me | 현재 로그인 사용자 조회 |
| GET | /api/library | 계정 라이브러리 조회 |
| PUT | /api/library | 계정 라이브러리 동기화 |
| PUT | /api/games/:id/best | 게임 최고 기록 갱신 |

## 데이터베이스
- `users`: 계정 이메일, 비밀번호 해시, 닉네임
- `sessions`: 사용자별 세션 토큰 해시와 만료 시각
- `library_items`: 사용자별 저장 게임
- `game_records`: 사용자별 게임 최고 기록
- `auth_attempts`: 가입·로그인 시도 제한 카운터

## 보안 적용 사항
- 비밀번호는 PBKDF2-HMAC-SHA-256, 100,000회 반복 및 개별 salt로 해시하여 저장합니다. 비밀번호 원문은 DB에 저장하지 않습니다.
- 32바이트 난수 세션 토큰을 발급하고 DB에는 SHA-256 해시만 저장합니다.
- 세션 만료는 발급 후 30일이며 로그아웃 시 현재 세션을 폐기합니다.
- 로그인은 IP·이메일 조합 기준 15분 동안 8회, 가입은 1시간 동안 5회로 제한합니다.
- CORS는 실제 GitHub Pages Origin만 허용합니다.
- 라이브러리와 기록 API는 유효한 세션이 있어야 사용할 수 있습니다.
- 프런트엔드 토큰은 브라우저 `sessionStorage` 또는 사용자가 '로그인 상태 유지'를 선택한 경우 `localStorage`에 저장됩니다. 이는 HttpOnly 쿠키보다 XSS에 취약할 수 있으므로 프런트엔드에 신뢰할 수 없는 스크립트를 추가하지 않아야 합니다.

## 아직 구현되지 않은 항목
- 이메일 주소 소유 확인
- 비밀번호 재설정 메일 발송
- 계정 삭제 및 개인정보 내보내기 화면
- 게임별 최고 기록의 프런트엔드 자동 동기화 (API는 준비됨)
- 다중 기기에서 동시 로그인 세션 관리 화면

## 운영 주소
- 로그인: `/account/login.html`
- 라이브러리: `/library/`
- API: `https://daemonscript-gaming-auth.youthdeveloper-github.workers.dev`
