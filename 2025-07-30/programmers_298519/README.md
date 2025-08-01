# [특정 조건을 만족하는 물고기별 수와 최대 길이 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/298519)

## 문제 설명

낚시앱에서 사용하는 `FISH_INFO` 테이블은 잡은 물고기들의 정보를 담고 있습니다. `FISH_INFO` 테이블의 구조는 다음과 같으며 `ID`, `FISH_TYPE`, `LENGTH`, `TIME`은 각각 잡은 물고기의 ID, 물고기의 종류(숫자), 잡은 물고기의 길이(cm), 물고기를 잡은 날짜를 나타냅니다.

| Column name | Type    | Nullable |
| ----------- | ------- | -------- |
| ID          | INTEGER | FALSE    |
| FISH_TYPE   | INTEGER | FALSE    |
| LENGTH      | FLOAT   | TRUE     |
| TIME        | DATE    | FALSE    |

단, 잡은 물고기의 길이가 10cm 이하일 경우에는 `LENGTH` 가 NULL 이며, `LENGTH` 에 NULL 만 있는 경우는 없습니다.

## 문제

`FISH_INFO`에서 평균 길이가 33cm 이상인 물고기들을 종류별로 분류하여 잡은 수, 최대 길이, 물고기의 종류를 출력하는 SQL문을 작성해주세요. 결과는 물고기 종류에 대해 오름차순으로 정렬해주시고, 10cm이하의 물고기들은 10cm로 취급하여 평균 길이를 구해주세요.

컬럼명은 물고기의 종류 'FISH_TYPE', 잡은 수 'FISH_COUNT', 최대 길이 'MAX_LENGTH'로 해주세요.

## 예시

예를 들어 `FISH_INFO` 테이블이 다음과 같다면

| ID  | FISH_TYPE | LENGTH | TIME       |
| --- | --------- | ------ | ---------- |
| 0   | 0         | 30     | 2021/12/04 |
| 1   | 0         | 50     | 2020/03/07 |
| 2   | 0         | 40     | 2020/03/07 |
| 3   | 1         | 30     | 2022/03/09 |
| 4   | 1         | NULL   | 2022/04/08 |
| 5   | 2         | 32     | 2020/04/28 |

물고기 종류가 0인 물고기들의 평균 길이는 (30 + 50 + 40) / 3 = 40cm 이고 물고기 종류가 1인 물고기들의 평균 길이는 (30 + 10) / 2 = 20cm 이며, 물고기 종류가 2인 물고기들의 평균 길이는 (32) / 1 = 32cm 입니다. 따라서 평균길이가 33cm 인 물고기 종류는 0 이므로, 총 잡은 수는 3마리, 최대 길이는 50cm 이므로 결과는 다음과 같아야 합니다.

| FISH_COUNT | MAX_LENGTH | FISH_TYPE |
| ---------- | ---------- | --------- |
| 3          | 50         | 0         |

---

## 문제 정보

| 난이도 | Lv. 3 |
| ------ | ----- |
| 정답률 | 75%   |

---

## 풀이

```SQL
SELECT
    COUNT(*) AS FISH_COUNT,
    MAX(LENGTH) AS MAX_LENGTH,
    FISH_TYPE
FROM FISH_INFO
GROUP BY FISH_TYPE
HAVING AVG(IFNULL(LENGTH, 10)) >= 33
ORDER BY FISH_TYPE;
```

---

## 결과

| 채점 결과        |
| ---------------- |
| 테스트 1 〉 통과 |
| 테스트 2 〉 통과 |
| 테스트 3 〉 통과 |
| 테스트 4 〉 통과 |
| 테스트 5 〉 통과 |
| 테스트 6 〉 통과 |

---
