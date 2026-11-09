# 1단계. 프로젝트 기본 구조와 배포

- 권장 모델: Sonnet 5.5 / effort medium
- 이유: 정형화된 설정 작업. 설계 판단이 적음.
- 읽을 파일: `00-overview.md`, 이 파일

## 작업
1. Vite + React + TypeScript 프로젝트 생성. vite-plugin-pwa, Dexie, Vitest 설치.
2. 하단 탭 4개(이번 주·장보기·레시피·기록)와 빈 화면. 라우팅은 해시 라우터(GitHub Pages 호환).
3. PWA manifest (이름 "주간 식단", 아이콘, standalone), 서비스워커로 앱 파일 오프라인 캐시.
4. GitHub Actions 워크플로: main 푸시 시 빌드 → GitHub Pages 배포. `base`는 `/weeklymenu/`.
5. npm 스크립트: `dev`, `build`, `test`, `validate:data`(3단계에서 채움, 지금은 빈 스크립트).

## 완료 기준
- `npm run build`, `npm test` 통과.
- PR 머지 후 Actions 배포 성공.

## 사용자 확인 필요 사항 (단계 끝에 반드시 알림)
1. 저장소 Settings → Pages → Source를 "GitHub Actions"로 설정 (Claude가 할 수 없음). 설정 화면 링크를 함께 보낼 것.
2. PR 승인·머지.
3. 안드로이드 크롬에서 배포 주소 열기 → 메뉴 "홈 화면에 추가" → 아이콘으로 실행되는지, 비행기 모드에서도 열리는지 확인.
