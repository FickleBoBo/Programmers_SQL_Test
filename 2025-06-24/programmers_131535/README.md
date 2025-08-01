# [조건에 맞는 회원수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131535)

## 문제 설명

다음은 어느 의류 쇼핑몰에 가입한 회원 정보를 담은 `USER_INFO` 테이블입니다. `USER_INFO` 테이블은 아래와 같은 구조로 되어있으며, `USER_ID`, `GENDER`, `AGE`, `JOINED`는 각각 회원 ID, 성별, 나이, 가입일을 나타냅니다.

| Column name | Type       | Nullable |
| ----------- | ---------- | -------- |
| USER_ID     | INTEGER    | FALSE    |
| GENDER      | TINYINT(1) | TRUE     |
| AGE         | INTEGER    | TRUE     |
| JOINED      | DATE       | FALSE    |

`GENDER` 컬럼은 비어있거나 0 또는 1의 값을 가지며 0인 경우 남자를, 1인 경우는 여자를 나타냅니다.

## 문제

`USER_INFO` 테이블에서 2021년에 가입한 회원 중 나이가 20세 이상 29세 이하인 회원이 몇 명인지 출력하는 SQL문을 작성해주세요.

## 예시

예를 들어 `USER_INFO` 테이블이 다음과 같다면

| USER_ID | GENDER | AGE  | JOINED     |
| ------- | ------ | ---- | ---------- |
| 1       | 1      | 26   | 2021-10-05 |
| 2       | 0      | NULL | 2021-11-25 |
| 3       | 1      | 22   | 2021-11-30 |
| 4       | 0      | 31   | 2021-12-03 |
| 5       | 0      | 28   | 2021-12-16 |
| 6       | 1      | 24   | 2022-01-03 |
| 7       | 1      | NULL | 2022-01-09 |

2021년에 가입한 회원 중 나이가 20세 이상 29세 이하인 회원은 `USER_ID` 가 1, 3, 5 인 회원들 이므로, 다음과 같이 결과가 나와야 합니다.

| USERS |
| ----- |
| 3     |

---

## 문제 정보

| 난이도 | Lv. 1 |
| ------ | ----- |
| 정답률 | 91%   |

---

## 풀이

```SQL
SELECT COUNT(*) AS USERS
FROM USER_INFO
WHERE YEAR(JOINED) = 2021 AND AGE BETWEEN 20 AND 29;
```

---

## 결과

![결과](./assets/스크린샷%202025-06-24%2023.15.46.png)

---
