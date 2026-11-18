# DaeMonScript Gaming 계정 시스템 설계

## 목표
- 이메일 기반 회원가입 및 로그인
- 닉네임, 계정 설정, 로그아웃
- 여러 기기에서 라이브러리와 게임 최고 기록 동기화
- 추후 Google 등 OAuth 로그인 확장

## 권장 구성
- Frontend: GitHub Pages의 정적 페이지
- API: Cloudflare Workers
- Database: Cloudflare D1
- Session: 서버가 발급하는 불투명한 세션 토큰을 Secure, HttpOnly, SameSite 쿠키로 관리
- Password: Workers에서 지원되는 검증된 비밀번호 해시 구현 사용. 평문 또는 단순 SHA 해시 저장 금지.

## API 초안
| Method | Endpoint | 기능 |
|---|---|---|
| POST | /api/auth/register | 이메일·비밀번호·닉네임 회원가입 |
| POST | /api/auth/login | 로그인 및 세션 발급 |
| POST | /api/auth/logout | 세션 폐기 |
| GET | /api/auth/me | 현재 로그인 사용자 |
| POST | /api/auth/password/reset | 재설정 요청 |
| GET | /api/library | 계정 라이브러리 조회 |
| PUT | /api/library | 라이브러리 동기화 |
| PUT | /api/games/:id/best | 게임 최고 기록 갱신 |

## D1 테이블 초안
- users: id, email_normalized UNIQUE, password_hash, nickname, created_at, updated_at
- sessions: id, user_id, token_hash UNIQUE, expires_at, created_at
- library_items: user_id, game_id, created_at (user_id + game_id UNIQUE)
- game_records: user_id, game_id, best_score, updated_at (user_id + game_id UNIQUE)
- password_reset_tokens: token_hash, user_id, expires_at, used_at

## 필수 보안 기준
- 비밀번호 원문은 저장하거나 로그에 남기지 않음
- 이메일 정규화 및 중복 가입 방지
- 로그인 시도 속도 제한, 일반화된 오류 메시지, CSRF 방어
- 세션 토큰은 충분한 난수로 생성하고 DB에는 해시만 저장
- HTTPS 전용 쿠키, 세션 만료·로그아웃 시 서버 측 폐기
- CORS는 실제 서비스 도메인만 허용
- 비밀번호 재설정은 일회용·짧은 만료시간 토큰 사용
- 계정 데이터 조회·수정은 반드시 소유자 검증
- 개인정보 최소 수집 및 삭제 요청 경로 마련

## 구현 순서
1. Cloudflare Worker 및 D1 바인딩 확인
2. D1 마이그레이션 적용
3. 회원가입·로그인·세션 API 구현
4. 프론트엔드 연결 및 오류 처리
5. 라이브러리·게임 기록 동기화
6. 보안 테스트 및 운영 배포

## 현재 상태
로그인 화면은 UI 미리보기이며 실제 인증은 비활성화되어 있습니다. Worker 계정·환경변수·D1 설정을 확인하기 전에는 실제 로그인 가능하다고 표시하지 않습니다.
