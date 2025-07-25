# [과일로 만든 아이스크림 고르기](https://school.programmers.co.kr/learn/courses/30/lessons/133025)

## 문제 설명

다음은 아이스크림 가게의 상반기 주문 정보를 담은 `FIRST_HALF` 테이블과 아이스크림 성분에 대한 정보를 담은 `ICECREAM_INFO` 테이블입니다. `FIRST_HALF` 테이블 구조는 다음과 같으며, `SHIPMENT_ID`, `FLAVOR`, `TOTAL_ORDER` 는 각각 아이스크림 공장에서 아이스크림 가게까지의 출하 번호, 아이스크림 맛, 상반기 아이스크림 총주문량을 나타냅니다. `FIRST_HALF` 테이블의 기본 키는 `FLAVOR`입니다.

| NAME        | TYPE       | NULLABLE |
| ----------- | ---------- | -------- |
| SHIPMENT_ID | INT(N)     | FALSE    |
| FLAVOR      | VARCHAR(N) | FALSE    |
| TOTAL_ORDER | INT(N)     | FALSE    |

`ICECREAM_INFO` 테이블 구조는 다음과 같으며, `FLAVOR`, `INGREDITENT_TYPE` 은 각각 아이스크림 맛, 아이스크림의 성분 타입을 나타냅니다. `INGREDIENT_TYPE`에는 아이스크림의 주 성분이 설탕이면 `sugar_based`라고 입력되고, 아이스크림의 주 성분이 과일이면 `fruit_based`라고 입력됩니다. `ICECREAM_INFO`의 기본 키는 `FLAVOR`입니다. `ICECREAM_INFO`테이블의 `FLAVOR`는 `FIRST_HALF` 테이블의 `FLAVOR`의 외래 키입니다.

| NAME            | TYPE       | NULLABLE |
| --------------- | ---------- | -------- |
| FLAVOR          | VARCHAR(N) | FALSE    |
| INGREDIENT_TYPE | VARCHAR(N) | FALSE    |

## 문제

상반기 아이스크림 총주문량이 3,000보다 높으면서 아이스크림의 주 성분이 과일인 아이스크림의 맛을 총주문량이 큰 순서대로 조회하는 SQL 문을 작성해주세요.

## 예시

예를 들어 `FIRST_HALF` 테이블이 다음과 같고

| SHIPMENT_ID | FLAVOR          | TOTAL_ORDER |
| ----------- | --------------- | ----------- |
| 101         | chocolate       | 3200        |
| 102         | vanilla         | 2800        |
| 103         | mint_chocolate  | 1700        |
| 104         | caramel         | 2600        |
| 105         | white_chocolate | 3100        |
| 106         | peach           | 2450        |
| 107         | watermelon      | 2150        |
| 108         | mango           | 2900        |
| 109         | strawberry      | 3100        |
| 110         | melon           | 3150        |
| 111         | orange          | 2900        |
| 112         | pineapple       | 2900        |

`ICECREAM_INFO` 테이블이 다음과 같다면

| FLAVOR          | INGREDIENT_TYPE |
| --------------- | --------------- |
| chocolate       | sugar_based     |
| vanilla         | sugar_based     |
| mint_chocolate  | sugar_based     |
| caramel         | sugar_based     |
| white_chocolate | sugar_based     |
| peach           | fruit_based     |
| watermelon      | fruit_based     |
| mango           | fruit_based     |
| strawberry      | fruit_based     |
| melon           | fruit_based     |
| orange          | fruit_based     |
| pineapple       | fruit_based     |

상반기 아이스크림 총주문량이 3,000보다 높은 아이스크림 맛은 chocolate, strawberry, melon, white_chocolate입니다. 이 중에 아이스크림의 주 성분이 과일인 아이스크림 맛은 strawberry와 melon이고 총주문량이 큰 순서대로 아이스크림 맛을 조회하면 melon, strawberry 순으로 조회되어야 합니다. 따라서 SQL 문을 실행하면 다음과 같이 나와야 합니다.

| FLAVOR     |
| ---------- |
| melon      |
| strawberry |

---

## 문제 정보

| 난이도 | Lv. 1 |
| ------ | ----- |
| 정답률 | 84%   |

---

## 풀이

```SQL
SELECT f.FLAVOR
FROM FIRST_HALF AS f
JOIN ICECREAM_INFO AS i
    ON f.FLAVOR = i.FLAVOR
WHERE f.TOTAL_ORDER > 3000 AND i.INGREDIENT_TYPE = "fruit_based"
ORDER BY f.TOTAL_ORDER DESC;
```

---

## 결과

![결과](./assets/스크린샷%202025-06-25%2020.13.17.png)

---
