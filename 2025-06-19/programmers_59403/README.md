# [동물의 아이디와 이름](https://school.programmers.co.kr/learn/courses/30/lessons/59403)

## 문제 설명

`ANIMAL_INS` 테이블은 동물 보호소에 들어온 동물의 정보를 담은 테이블입니다. `ANIMAL_INS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `INTAKE_CONDITION`, `NAME`, `SEX_UPON_INTAKE`는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.

| NAME             | TYPE       | NULLABLE |
| ---------------- | ---------- | -------- |
| ANIMAL_ID        | VARCHAR(N) | FALSE    |
| ANIMAL_TYPE      | VARCHAR(N) | FALSE    |
| DATETIME         | DATETIME   | FALSE    |
| INTAKE_CONDITION | VARCHAR(N) | FALSE    |
| NAME             | VARCHAR(N) | TRUE     |
| SEX_UPON_INTAKE  | VARCHAR(N) | FALSE    |

동물 보호소에 들어온 모든 동물의 아이디와 이름을 `ANIMAL_ID`순으로 조회하는 SQL문을 작성해주세요. SQL을 실행하면 다음과 같이 출력되어야 합니다.

| ANIMAL_ID | NAME         |
| --------- | ------------ |
| A349996   | Sugar        |
| A350276   | Jewel        |
| A350375   | Meo          |
| A352555   | Harley       |
| A352713   | Gia          |
| A352872   | Peanutbutter |
| A353259   | Bj           |

((이하 생략))

---

## 문제 정보

| 난이도 | Lv. 1 |
| ------ | ----- |
| 정답률 | 91%   |

---

## 풀이

```SQL
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

---

## 결과

![결과](./assets/스크린샷%202025-06-19%2013.09.07.png)

---
