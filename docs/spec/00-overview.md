# 00. 공통 개요 (모든 단계에서 읽음)

## 제품
- 안드로이드 크롬에서 쓰는 개인용 PWA (홈 화면 추가). 사용자 1명.
- 미리 만든 메뉴 라이브러리로 주간 저녁 식단(월~일)을 자동 추천 → 사용자가 수정 → 장보기목록 자동 계산 → 마트에서 체크 → 레시피 확인.
- 가족: 어른 2 + 딸 1(2026-11 기준 30개월). 분량 고정.

## 기술 스택
| 구성 | 선택 |
| --- | --- |
| 앱 | Vite + React + TypeScript, PWA(vite-plugin-pwa) |
| 상태·로컬 저장 | IndexedDB (Dexie). 1~6단계는 로컬 전용 |
| 서버 저장 | Firebase Spark 무료 요금제: Firestore + Google 로그인 (7단계) |
| 호스팅 | GitHub Pages, GitHub Actions로 배포 |
| 테스트 | Vitest (로직 단위 테스트만. E2E는 생략) |

## 화면 (하단 탭 4개)
이번 주 / 장보기 / 레시피 / 기록

## 메뉴 규칙 (라이브러리 작성 + 자동 추천 공통)
1. 매운 음식 금지.
2. 작업 시간(기다리는 시간 제외) 30분 이내, 총 조리 시간(기다림 포함) 약 90분 이내.
3. 매끼 단백질 충분 + 채소 포함. 아이용으로 부드럽게 조리. 한그릇·유럽식 선호.
4. 추천 시: 최근 2주 내 메뉴 제외 / 생선 주 1회 이상 / 단백질 종류 분산 / 요리 종류(한식·일식·이탈리아식·기타유럽식·구이찜) 중 한 종류 주 3회 이하.
5. 주말(토·일)은 총 조리 시간 45분 이내 메뉴만.

## 데이터 모델 (요약, 정식 정의는 `src/types.ts`)
- Recipe: id, name, cuisine, protein, activeMin, totalMin, ingredients[{ingredientId, qty, unit}], steps[], tags[]
- Ingredient(사전): id, name, unit, section(채소·정육·수산·유제품·가공·양념·기타), pantry(상비 양념 여부)
- WeekPlan: weekStart(월요일 YYYY-MM-DD), days[7] = recipeId
- ShoppingList: weekStart, items[{name, qty, unit, section, checked, source: auto|manual, removed}]
- Review: recipeId, date, rating 1~5, memo

## 단계 목록
| 단계 | 파일 | 권장 모델 | 사용자 개입 |
| --- | --- | --- | --- |
| 1 | 01-setup.md | Sonnet 5.5 | Pages 설정, 폰에서 열어보기 |
| 2 | 02-data-schema.md | Opus 5.5 | 매장 구역·단위 확인 |
| 3 | 03-recipe-library.md | Sonnet 5.5 | 메뉴 목록 승인, 레시피 샘플 확인 |
| 4 | 04-weekly-plan.md | Sonnet 5.5 | 추천 결과 4주치 확인 |
| 5 | 05-shopping-list.md | Sonnet 5.5 | 실제 장보기 1회 |
| 6 | 06-recipe-history.md | Haiku 5.5 | 화면 확인 |
| 7 | 07-firebase-sync.md | Opus 5.5 | Firebase 프로젝트 생성 |
| 8 | 08-reviews-export.md | Haiku 5.5 | 평가·내보내기 확인 |

1~6단계 완료 시점이 MVP(실사용 가능)다.
