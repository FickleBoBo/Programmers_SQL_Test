# [카테고리 별 도서 판매량 집계하기](https://school.programmers.co.kr/learn/courses/30/lessons/144855)

## 문제 설명

다음은 어느 한 서점에서 판매중인 도서들의 도서 정보(`BOOK`), 판매 정보(`BOOK_SALES`) 테이블입니다.

`BOOK` 테이블은 각 도서의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

| Column name    | Type       | Nullable | Description                             |
| -------------- | ---------- | -------- | --------------------------------------- |
| BOOK_ID        | INTEGER    | FALSE    | 도서 ID                                 |
| CATEGORY       | VARCHAR(N) | FALSE    | 카테고리 (경제, 인문, 소설, 생활, 기술) |
| AUTHOR_ID      | INTEGER    | FALSE    | 저자 ID                                 |
| PRICE          | INTEGER    | FALSE    | 판매가 (원)                             |
| PUBLISHED_DATE | DATE       | FALSE    | 출판일                                  |

`BOOK_SALES` 테이블은 각 도서의 날짜 별 판매량 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

| Column name | Type    | Nullable | Description |
| ----------- | ------- | -------- | ----------- |
| BOOK_ID     | INTEGER | FALSE    | 도서 ID     |
| SALES_DATE  | DATE    | FALSE    | 판매일      |
| SALES       | INTEGER | FALSE    | 판매량      |

## 문제

`2022년 1월`의 카테고리 별 도서 판매량을 합산하고, 카테고리(`CATEGORY`), 총 판매량(`TOTAL_SALES`) 리스트를 출력하는 SQL문을 작성해주세요.
결과는 카테고리명을 기준으로 오름차순 정렬해주세요.

## 예시

예를 들어 `BOOK` 테이블과 `BOOK_SALES` 테이블이 다음과 같다면

| BOOK_ID | CATEGORY | AUTHOR_ID | PRICE | PUBLISHED_DATE |
| ------- | -------- | --------- | ----- | -------------- |
| 1       | 인문     | 1         | 10000 | 2020-01-01     |
| 2       | 경제     | 1         | 9000  | 2021-02-05     |
| 3       | 경제     | 2         | 9000  | 2021-03-11     |

| BOOK_ID | SALES_DATE | SALES |
| ------- | ---------- | ----- |
| 1       | 2022-01-01 | 2     |
| 2       | 2022-01-02 | 3     |
| 1       | 2022-01-05 | 1     |
| 2       | 2022-01-20 | 5     |
| 2       | 2022-01-21 | 6     |
| 3       | 2022-01-22 | 2     |
| 2       | 2022-02-11 | 3     |

2022년 1월의 도서 별 총 판매량은 도서 ID 가 1 인 도서가 총 3권, 도서 ID 가 2 인 도서가 총 14권 이고, 도서 ID 가 3 인 도서가 총 2권 입니다.

카테고리 별로 판매량을 집계한 결과는 다음과 같습니다.

| CATEGORY | TOTAL_SALES |
| -------- | ----------- |
| 인문     | 3           |
| 경제     | 16          |

카테고리명을 오름차순으로 정렬하면 다음과 같이 나와야 합니다.

| CATEGORY | TOTAL_SALES |
| -------- | ----------- |
| 경제     | 16          |
| 인문     | 3           |

---

## 문제 정보

| 난이도 | Lv. 3 |
| ------ | ----- |
| 정답률 | 88%   |

---

## 풀이

```SQL
SELECT
    B.CATEGORY,
    SUM(S.SALES) AS TOTAL_SALES
FROM BOOK AS B
JOIN BOOK_SALES AS S
    ON B.BOOK_ID = S.BOOK_ID
WHERE S.SALES_DATE LIKE "2022-01%"
GROUP BY B.CATEGORY
ORDER BY B.CATEGORY;
```

---

## 결과

![결과](./assets/스크린샷%202025-07-13%2022.17.45.png)

---
