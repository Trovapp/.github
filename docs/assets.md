# 소개 이미지 기록

## 앱 캡처

- 촬영일: 2026-11-05 (KST)
- 기기: iPhone 17 Pro 시뮬레이터, iOS 26.5
- 앱 소스: `Trovapp/trova-app` main `8197bbf70e041e5a1fc78d2b4e227630e8f877df`
- 방식: 실제 네이티브 앱을 실행하고 UI를 조작한 뒤 `xcrun simctl io … screenshot`으로 촬영
- 데이터: 로컬 개발 API의 기존 QA 계정·장소·일정·여행. 촬영을 위한 새 분석·AI 요청이나 여행 생성은 하지 않음.
- 상태 표시줄은 촬영용으로 9:41·배터리 100%로 통일. 화면 콘텐츠는 원본 캡처이며 합성·생성하지 않음.
- 온보딩 미리보기와 기존 QA 인증 방식은 별도 임시 체크아웃에만 적용. 앱 저장소에는 반영하지 않음.

| 파일 | 내용 |
| --- | --- |
| `profile/assets/screenshots/01-onboarding.png` | 첫 실행 소개 |
| `profile/assets/screenshots/02-sharing-guide.png` | 공유 방법 데모 |
| `profile/assets/screenshots/03-home.png` | 홈·준비된 일정 |
| `profile/assets/screenshots/04-place-map.png` | 영상에서 추출한 장소·지도 |
| `profile/assets/screenshots/05-ai-draft.png` | 기존 AI 일정 초안 |
| `profile/assets/screenshots/06-trip.png` | 기존 여행의 지도·편집 기능 |

## 브랜드

`profile/assets/ticket-mascot.png`는 앱 저장소의 기존 브랜드 자산(`assets/brand/ticket-mascot@3x.png`)입니다.

## 아키텍처

`profile/assets/architecture.png`는 코드와 ADR을 기준으로 내장 image_gen 도구로 생성한 개념도입니다. 생성 프롬프트는 `architecture-prompt.txt`에 기록합니다.

- API → 외부 Aiven Kafka → 분석 작업. 전송 실패 시 내부 async로 전달.
- Python 분석은 별도 서버가 아니라 API 서버가 실행하는 보조 프로세스.
- Trip Planner는 별도 배포 서비스가 아니라 백엔드 내부 모듈.
- PostgreSQL·pgvector는 외부 Supabase에 위치.
- Prometheus·Grafana는 운영 서버 밖의 로컬 환경에서 SSH 터널로 수집.
- 앱의 지도 SDK 통신, 인증 공급자, 정적 웹 호스팅, 푸시 전달 등은 생략한 개념도.
