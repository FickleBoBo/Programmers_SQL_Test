# [조건에 맞는 도서와 저자 리스트 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/144854)

## 문제 설명

다음은 어느 한 서점에서 판매중인 도서들의 도서 정보(`BOOK`), 저자 정보(`AUTHOR`) 테이블입니다.

`BOOK` 테이블은 각 도서의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

| Column name    | Type       | Nullable | Description                             |
| -------------- | ---------- | -------- | --------------------------------------- |
| BOOK_ID        | INTEGER    | FALSE    | 도서 ID                                 |
| CATEGORY       | VARCHAR(N) | FALSE    | 카테고리 (경제, 인문, 소설, 생활, 기술) |
| AUTHOR_ID      | INTEGER    | FALSE    | 저자 ID                                 |
| PRICE          | INTEGER    | FALSE    | 판매가 (원)                             |
| PUBLISHED_DATE | DATE       | FALSE    | 출판일                                  |

`AUTHOR` 테이블은 도서의 저자의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.

| Column name | Type       | Nullable | Description |
| ----------- | ---------- | -------- | ----------- |
| AUTHOR_ID   | INTEGER    | FALSE    | 저자 ID     |
| AUTHOR_NAME | VARCHAR(N) | FALSE    | 저자명      |

## 문제

`'경제'` 카테고리에 속하는 도서들의 도서 ID(`BOOK_ID`), 저자명(`AUTHOR_NAME`), 출판일(`PUBLISHED_DATE`) 리스트를 출력하는 SQL문을 작성해주세요.
결과는 출판일을 기준으로 오름차순 정렬해주세요.

## 예시

예를 들어 `BOOK` 테이블과 `AUTHOR` 테이블이 다음과 같다면

| BOOK_ID | CATEGORY | AUTHOR_ID | PRICE | PUBLISHED_DATE |
| ------- | -------- | --------- | ----- | -------------- |
| 1       | 인문     | 1         | 10000 | 2020-01-01     |
| 2       | 경제     | 1         | 9000  | 2021-04-11     |
| 3       | 경제     | 2         | 11000 | 2021-02-05     |

| AUTHOR_ID | AUTHOR_NAME |
| --------- | ----------- |
| 1         | 홍길동      |
| 2         | 김영호      |

`'경제'` 카테고리에 속하는 도서는 도서 ID가 2, 3인 도서이고, 출판일을 기준으로 오름차순으로 정렬하면 다음과 같은 결과가 나와야 합니다.

| BOOK_ID | AUTHOR_NAME | PUBLISHED_DATE |
| ------- | ----------- | -------------- |
| 3       | 김영호      | 2021-02-05     |
| 2       | 홍길동      | 2021-04-11     |

## 주의사항

`PUBLISHED_DATE`의 데이트 포맷이 예시와 동일해야 정답처리 됩니다.

---

## 문제 정보

| 난이도 | Lv. 2 |
| ------ | ----- |
| 정답률 | 88%   |

---

## 풀이

```SQL
SELECT b.BOOK_ID, a.AUTHOR_NAME, DATE_FORMAT(b.PUBLISHED_DATE, "%Y-%m-%d") AS PUBLISHED_DATE
FROM BOOK AS b
JOIN AUTHOR AS a
    ON b.AUTHOR_ID = a.AUTHOR_ID
WHERE b.CATEGORY = "경제"
ORDER BY b.PUBLISHED_DATE;
```

---

## 결과

![결과](./assets/스크린샷%202025-06-19%2019.38.55.png)

---
