# [대장균들의 자식의 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/299305)

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

대장균 개체의 ID(`ID`)와 자식의 수(`CHILD_COUNT`)를 출력하는 SQL 문을 작성해주세요. 자식이 없다면 자식의 수는 0으로 출력해주세요. 이때 결과는 개체의 ID 에 대해 오름차순 정렬해주세요.

## 예시

예를 들어 `ECOLI_DATA` 테이블이 다음과 같다면

| ID  | PARENT_ID | SIZE_OF_COLONY | DIFFERENTIATION_DATE | GENOTYPE |
| --- | --------- | -------------- | -------------------- | -------- |
| 1   | NULL      | 10             | 2019/01/01           | 5        |
| 2   | NULL      | 2              | 2019/01/01           | 3        |
| 3   | 1         | 100            | 2020/01/01           | 4        |
| 4   | 2         | 17             | 2020/01/01           | 4        |
| 5   | 2         | 10             | 2020/01/01           | 6        |
| 6   | 4         | 101            | 2021/01/01           | 22       |

ID 1인 개체의 자식은 ID 3으로 1개 ID 2인 개체의 자식은 ID 4,5 로 2개 ID 4인 개체의 자식은 ID 6으로 1개이며 나머지 개체들은 자식이 없으므로 ID 에 대해 오름차순 정렬하면 결과는 다음과 같아야 합니다.

| ID  | CHILD_COUNT |
| --- | ----------- |
| 1   | 1           |
| 2   | 2           |
| 3   | 0           |
| 4   | 1           |
| 5   | 0           |
| 6   | 0           |

---

## 문제 정보

| 난이도 | Lv. 3 |
| ------ | ----- |
| 정답률 | 71%   |

---

## 풀이

```SQL
SELECT ED1.ID, COUNT(ED2.PARENT_ID) AS CHILD_COUNT
FROM ECOLI_DATA AS ED1
LEFT JOIN ECOLI_DATA AS ED2
    ON ED1.ID = ED2.PARENT_ID
GROUP BY ED1.ID
ORDER BY ED1.ID;
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
