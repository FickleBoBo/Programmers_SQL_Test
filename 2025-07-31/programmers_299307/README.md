# [대장균의 크기에 따라 분류하기 1](https://school.programmers.co.kr/learn/courses/30/lessons/299307)

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

대장균 개체의 크기가 100 이하라면 'LOW', 100 초과 1000 이하라면 'MEDIUM', 1000 초과라면 'HIGH' 라고 분류합니다. 대장균 개체의 ID(`ID`) 와 분류(`SIZE`)를 출력하는 SQL 문을 작성해주세요.이때 결과는 개체의 ID 에 대해 오름차순 정렬해주세요.

## 예시

예를 들어 `ECOLI_DATA` 테이블이 다음과 같다면

| ID  | PARENT_ID | SIZE_OF_COLONY | DIFFERENTIATION_DATE | GENOTYPE |
| --- | --------- | -------------- | -------------------- | -------- |
| 1   | NULL      | 17             | 2019/01/01           | 5        |
| 2   | NULL      | 150            | 2019/01/01           | 3        |
| 3   | 1         | 4000           | 2020/01/01           | 4        |

대장균 개체 ID(`ID`) 1,2,3 에 대해 개체의 크기는 각각 17, 150, 4000 이므로 분류된 이름은 각각 'LOW', 'MEDIUM', 'HIGH' 입니다. 따라서 결과를 개체의 ID 에 대해 오름차순 정렬하면 다음과 같아야 합니다.

| ID  | SIZE   |
| --- | ------ |
| 1   | LOW    |
| 2   | MEDIUM |
| 3   | HIGH   |

---

## 문제 정보

| 난이도 | Lv. 3 |
| ------ | ----- |
| 정답률 | 82%   |

---

## 풀이

```SQL
SELECT
    ID,
    CASE
        WHEN SIZE_OF_COLONY > 1000 THEN "HIGH"
        WHEN SIZE_OF_COLONY > 100 THEN "MEDIUM"
        ELSE "LOW"
    END AS SIZE
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
