# 2단계. 데이터 구조와 재료 사전

- 권장 모델: Opus 5.5 / effort high
- 이유: 이후 모든 단계가 이 구조에 의존. 장보기 합산 정확도가 재료 사전의 단위 설계에 달려 있어 판단 비용이 큼. 한 번만 하므로 토큰 총량은 작음.
- 읽을 파일: `00-overview.md`, 이 파일, `src/` 디렉터리 목록만

## 작업
1. `src/types.ts`: Recipe, Ingredient, WeekPlan, ShoppingList, ShoppingItem, Review 타입 정의.
   - Recipe에 cuisine(korean·japanese·italian·european·grill_steam), protein(beef·pork·chicken·fish·shellfish·egg_tofu 등), activeMin, totalMin 필수.
2. `src/data/ingredients.json`: 재료 사전. 재료마다 표준 단위 1개(g·개·ml·모·단 등)와 매장 구역, 상비 양념 여부.
   - 같은 재료가 레시피마다 다른 단위로 쓰이지 않도록 표준 단위만 허용.
3. `scripts/validate-data.ts`: 모든 레시피가 스키마에 맞는지, 재료 id가 사전에 있는지, 단위가 표준 단위인지, activeMin ≤ 30, totalMin ≤ 100 검사. `npm run validate:data`에 연결.
4. Dexie DB 스키마(weekPlans, shoppingLists, reviews) 정의.
5. 장보기 합산 함수 `aggregateIngredients(recipes)` 와 단위 테스트.

## 완료 기준
- 검증 스크립트가 샘플 레시피 2개로 통과·실패를 각각 정확히 판정.
- 합산 테스트 통과 (같은 재료 합산, 상비 양념은 "확인" 항목으로 분리).

## 사용자 확인 필요 사항
1. 매장 구역 목록과 순서가 실제 다니는 마트 동선과 맞는지 (예: 채소 → 정육 → 수산 → 유제품 → 가공 → 양념).
2. 상비 양념으로 분류한 목록(소금·간장·올리브유 등)이 맞는지. 여기 들어간 재료는 장보기목록에 자동으로 안 들어감.
3. 표준 단위 예시 10개 정도를 보여주고, 장볼 때 이해하기 쉬운 단위인지 (예: 양파 "개", 소고기 "g").
4. PR 승인·머지.
