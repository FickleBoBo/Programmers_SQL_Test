# [대장균의 크기에 따라 분류하기 2](https://school.programmers.co.kr/learn/courses/30/lessons/301649)

## 문제 설명

대장균들은 일정 주기로 분화하며, 분화를 시작한 개체를 부모 개체, 분화가 되어 나온 개체를 자식 개체라고 합니다.
다음은 실험실에서 배양한 대장균들의 정보를 담은 `ECOLI_DATA` 테이블입니다. `ECOLI_DATA` 테이블의 구조는 다음과 같으며, `ID`, `PARENT_ID`, `SIZE_OF_COLONY`, `DIFFERENTIATION_DATE`, `GENOTYPE` 은 각각 대장균 개체의 ID, 부모 개체의 ID, 개체의 크기, 분화되어 나온 날짜, 개체의 형질을 나타냅니다.

| Column name          | Type    | Nullable |
| -------------------- | ------- | -------- |
| ID                   | INTEGER | FALSE    |
| PARENT_ID            | INTEGER | TRUE     |
| SIZE_OF_COLONY       | INTEGER | FALSE    |
| DIFFERENTIATION_DATE | DATE    | FALSE    |
| GENOTYPE             | INTEGER | FALSE    |

최초의 대장균 개체의 `PARENT_ID` 는 NULL 값입니다.

## 문제

대장균 개체의 크기를 내름차순으로 정렬했을 때 상위 0% ~ 25% 를 'CRITICAL', 26% ~ 50% 를 'HIGH', 51% ~ 75% 를 'MEDIUM', 76% ~ 100% 를 'LOW' 라고 분류합니다. 대장균 개체의 ID(`ID`) 와 분류된 이름(`COLONY_NAME`)을 출력하는 SQL 문을 작성해주세요. 이때 결과는 개체의 ID 에 대해 오름차순 정렬해주세요 . 단, 총 데이터의 수는 4의 배수이며 같은 사이즈의 대장균 개체가 서로 다른 이름으로 분류되는 경우는 없습니다.

## 예시

예를 들어 `ECOLI_DATA` 테이블이 다음과 같다면

| ID  | PARENT_ID | SIZE_OF_COLONY | DIFFERENTIATION_DATE | GENOTYPE |
| --- | --------- | -------------- | -------------------- | -------- |
| 1   | NULL      | 10             | 2019/01/01           | 5        |
| 2   | NULL      | 2              | 2019/01/01           | 3        |
| 3   | 1         | 100            | 2020/01/01           | 4        |
| 4   | 2         | 16             | 2020/01/01           | 4        |
| 5   | 2         | 17             | 2020/01/01           | 6        |
| 6   | 4         | 101            | 2021/01/01           | 22       |
| 7   | 6         | 101            | 2022/01/01           | 23       |
| 8   | 6         | 1              | 2022/01/01           | 27       |

기준에 의해 분류된 대장균들의 ID는 다음과 같습니다.

CRITICAL (상위 0% ~ 25%) : ID 6, ID 7  
HIGH (상위 26% ~ 50%) : ID 3, ID 5  
MEDIUM (상위 51% ~ 75%) : ID 1, ID 4  
LOW (상위 76% ~ 100%) : ID 2, ID 8

따라서 결과를 ID 에 대해 오름차순 정렬하면 다음과 같아야 합니다.

| ID  | COLONY_NAME |
| --- | ----------- |
| 1   | MEDIUM      |
| 2   | LOW         |
| 3   | HIGH        |
| 4   | MEDIUM      |
| 5   | HIGH        |
| 6   | CRITICAL    |
| 7   | CRITICAL    |
| 8   | LOW         |

---

## 문제 정보

| 난이도 | Lv. 3 |
| ------ | ----- |
| 정답률 | 59%   |

---

## 풀이

```SQL
SELECT
    ID,
    CASE
        WHEN PERCENT_RANK() OVER (ORDER BY SIZE_OF_COLONY) >= 0.75 THEN "CRITICAL"
        WHEN PERCENT_RANK() OVER (ORDER BY SIZE_OF_COLONY) >= 0.50 THEN "HIGH"
        WHEN PERCENT_RANK() OVER (ORDER BY SIZE_OF_COLONY) >= 0.25 THEN "MEDIUM"
        ELSE "LOW"
    END AS COLONY_NAME
FROM ECOLI_DATA
ORDER BY ID;
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
