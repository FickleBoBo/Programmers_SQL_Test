# [분기별 분화된 대장균의 개체 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/299308)

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

각 분기(`QUARTER`)별 분화된 대장균의 개체의 총 수(`ECOLI_COUNT`)를 출력하는 SQL 문을 작성해주세요. 이때 각 분기에는 'Q' 를 붙이고 분기에 대해 오름차순으로 정렬해주세요. 대장균 개체가 분화되지 않은 분기는 없습니다.

## 예시

예를 들어 `ECOLI_DATA` 테이블이 다음과 같다면

| ID  | PARENT_ID | SIZE_OF_COLONY | DIFFERENTIATION_DATE | GENOTYPE |
| --- | --------- | -------------- | -------------------- | -------- |
| 1   | NULL      | 10             | 2019/01/01           | 5        |
| 2   | NULL      | 2              | 2019/05/01           | 3        |
| 3   | 1         | 100            | 2020/01/01           | 4        |
| 4   | 2         | 17             | 2022/04/01           | 4        |
| 5   | 2         | 10             | 2020/09/01           | 6        |
| 6   | 4         | 101            | 2021/12/01           | 22       |

각 분기별로 분화된 대장균 개체는 다음과 같습니다.

1분기 : ID 1, ID 3  
2분기 : ID 2, ID 4  
3분기 : ID 5  
4분기 : ID 6

따라서 결과는 다음과 같아야 합니다

| QUARTER | ECOLI_COUNT |
| ------- | ----------- |
| 1Q      | 2           |
| 2Q      | 2           |
| 3Q      | 1           |
| 4Q      | 1           |

---

## 문제 정보

| 난이도 | Lv. 2 |
| ------ | ----- |
| 정답률 | 69%   |

---

## 풀이

```SQL
SELECT
    CONCAT(QUARTER(DIFFERENTIATION_DATE), "Q") AS QUARTER,
    COUNT(*) AS ECOLI_COUNT
FROM ECOLI_DATA
GROUP BY QUARTER
ORDER BY QUARTER;
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
