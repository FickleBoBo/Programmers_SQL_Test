# [중성화 여부 파악하기](https://school.programmers.co.kr/learn/courses/30/lessons/59409)

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

보호소의 동물이 중성화되었는지 아닌지 파악하려 합니다. 중성화된 동물은 `SEX_UPON_INTAKE` 컬럼에 'Neutered' 또는 'Spayed'라는 단어가 들어있습니다. 동물의 아이디와 이름, 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성해주세요. 이때 중성화가 되어있다면 'O', 아니라면 'X'라고 표시해주세요.

## 예시

예를 들어 `ANIMAL_INS` 테이블이 다음과 같다면

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME      | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | --------- | --------------- |
| A355753   | Dog         | 2015-09-10 13:14:00 | Normal           | Elijah    | Neutered Male   |
| A373219   | Cat         | 2014-07-29 11:43:00 | Normal           | Ella      | Spayed Female   |
| A382192   | Dog         | 2015-03-13 13:14:00 | Normal           | Maxwell 2 | Intact Male     |

- 중성화한 동물: Elijah, Ella
- 중성화하지 않은 동물: Maxwell 2

따라서 SQL문을 실행하면 다음과 같이 나와야 합니다.

| ANIMAL_ID | NAME      | 중성화 |
| --------- | --------- | ------ |
| A355753   | Elijah    | O      |
| A373219   | Ella      | O      |
| A382192   | Maxwell 2 | X      |

※ 컬럼 이름은 일치하지 않아도 됩니다.

---

## 문제 정보

| 난이도 | Lv. 2 |
| ------ | ----- |
| 정답률 | 90%   |

---

## 풀이

```SQL
SELECT
    ANIMAL_ID,
    NAME,
    IF(SEX_UPON_INTAKE LIKE "%Neutered%" OR SEX_UPON_INTAKE LIKE "%Spayed%", "O", "X") AS "중성화"
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

```SQL
SELECT
    ANIMAL_ID,
    NAME,
    CASE
        WHEN SEX_UPON_INTAKE LIKE "%Neutered%" OR SEX_UPON_INTAKE LIKE "%Spayed%" THEN "O"
        ELSE "X"
    END AS "중성화"
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

---

## 결과

![결과](./assets/스크린샷%202025-06-20%2010.37.55.png)
![결과](./assets/스크린샷%202025-06-20%2010.38.38.png)

---
