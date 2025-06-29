# [재구매가 일어난 상품과 회원 리스트 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131536)

## 문제 설명

다음은 어느 의류 쇼핑몰의 온라인 상품 판매 정보를 담은 `ONLINE_SALE` 테이블 입니다. `ONLINE_SALE` 테이블은 아래와 같은 구조로 되어있으며 `ONLINE_SALE_ID`, `USER_ID`, `PRODUCT_ID`, `SALES_AMOUNT`, `SALES_DATE`는 각각 온라인 상품 판매 ID, 회원 ID, 상품 ID, 판매량, 판매일을 나타냅니다.

| Column name    | Type    | Nullable |
| -------------- | ------- | -------- |
| ONLINE_SALE_ID | INTEGER | FALSE    |
| USER_ID        | INTEGER | FALSE    |
| PRODUCT_ID     | INTEGER | FALSE    |
| SALES_AMOUNT   | INTEGER | FALSE    |
| SALES_DATE     | DATE    | FALSE    |

동일한 날짜, 회원 ID, 상품 ID 조합에 대해서는 하나의 판매 데이터만 존재합니다.

## 문제

`ONLINE_SALE` 테이블에서 동일한 회원이 동일한 상품을 재구매한 데이터를 구하여, 재구매한 회원 ID와 재구매한 상품 ID를 출력하는 SQL문을 작성해주세요. 결과는 회원 ID를 기준으로 오름차순 정렬해주시고 회원 ID가 같다면 상품 ID를 기준으로 내림차순 정렬해주세요.

## 예시

예를 들어 `ONLINE_SALE` 테이블이 다음과 같다면

| ONLINE_SALE_ID | USER_ID | PRODUCT_ID | SALES_AMOUNT | SALES_DATE |
| -------------- | ------- | ---------- | ------------ | ---------- |
| 1              | 1       | 3          | 2            | 2022-02-25 |
| 2              | 1       | 4          | 1            | 2022-03-01 |
| 4              | 2       | 4          | 2            | 2022-03-12 |
| 3              | 1       | 3          | 3            | 2022-03-31 |
| 5              | 3       | 5          | 1            | 2022-04-03 |
| 6              | 2       | 4          | 1            | 2022-04-06 |
| 2              | 1       | 4          | 2            | 2022-05-11 |

`USER_ID` 가 1인 유저가 `PRODUCT_ID` 가 3, 4인 상품들을 재구매하고, `USER_ID` 가 2인 유저가 `PRODUCT_ID` 가 4인 상품을 재구매 하였으므로, 다음과 같이 결과가 나와야합니다.

| USER_ID | PRODUCT_ID |
| ------- | ---------- |
| 1       | 4          |
| 1       | 3          |
| 2       | 4          |

---

## 문제 정보

| 난이도 | Lv. 2 |
| ------ | ----- |
| 정답률 | 78%   |

---

## 풀이

```SQL
SELECT USER_ID, PRODUCT_ID
FROM ONLINE_SALE
GROUP BY USER_ID, PRODUCT_ID
HAVING COUNT(*) >= 2
ORDER BY USER_ID, PRODUCT_ID DESC;
```

---

## 결과

![결과](./assets/스크린샷%202025-06-27%2020.13.05.png)

---
