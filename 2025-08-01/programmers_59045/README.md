# [보호소에서 중성화한 동물](https://school.programmers.co.kr/learn/courses/30/lessons/59045)

## 문제 설명

`ANIMAL_INS` 테이블은 동물 보호소에 들어온 동물의 정보를 담은 테이블입니다. `ANIMAL_INS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `INTAKE_CONDITION`, `NAME`, `SEX_UPON_INTAKE`는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.

| Column name      | Type       | Nullable |
| ---------------- | ---------- | -------- |
| ANIMAL_ID        | VARCHAR(N) | FALSE    |
| ANIMAL_TYPE      | VARCHAR(N) | FALSE    |
| DATETIME         | DATETIME   | FALSE    |
| INTAKE_CONDITION | VARCHAR(N) | FALSE    |
| NAME             | VARCHAR(N) | TRUE     |
| SEX_UPON_INTAKE  | VARCHAR(N) | FALSE    |

`ANIMAL_OUTS` 테이블은 동물 보호소에서 입양 보낸 동물의 정보를 담은 테이블입니다. `ANIMAL_OUTS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `NAME`, `SEX_UPON_OUTCOME`는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다. `ANIMAL_OUTS` 테이블의 `ANIMAL_ID`는 `ANIMAL_INS`의 `ANIMAL_ID`의 외래 키입니다.

| Column name      | Type       | Nullable |
| ---------------- | ---------- | -------- |
| ANIMAL_ID        | VARCHAR(N) | FALSE    |
| ANIMAL_TYPE      | VARCHAR(N) | FALSE    |
| DATETIME         | DATETIME   | FALSE    |
| NAME             | VARCHAR(N) | TRUE     |
| SEX_UPON_OUTCOME | VARCHAR(N) | FALSE    |

보호소에서 중성화 수술을 거친 동물 정보를 알아보려 합니다. 보호소에 들어올 당시에는 중성화1되지 않았지만, 보호소를 나갈 당시에는 중성화된 동물의 아이디와 생물 종, 이름을 조회하는 아이디 순으로 조회하는 SQL 문을 작성해주세요.

## 예시

예를 들어, `ANIMAL_INS` 테이블과 `ANIMAL_OUTS` 테이블이 다음과 같다면

`ANIMAL_INS`

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME      | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | --------- | --------------- |
| A367438   | Dog         | 2015-09-10 16:01:00 | Normal           | Cookie    | Spayed Female   |
| A382192   | Dog         | 2015-03-13 13:14:00 | Normal           | Maxwell 2 | Intact Male     |
| A405494   | Dog         | 2014-05-16 14:17:00 | Normal           | Kaila     | Spayed Female   |
| A410330   | Dog         | 2016-09-11 14:09:00 | Sick             | Chewy     | Intact Female   |

`ANIMAL_OUTS`

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | NAME      | SEX_UPON_OUTCOME |
| --------- | ----------- | ------------------- | --------- | ---------------- |
| A367438   | Dog         | 2015-09-12 13:30:00 | Cookie    | Spayed Female    |
| A382192   | Dog         | 2015-03-16 13:46:00 | Maxwell 2 | Neutered Male    |
| A405494   | Dog         | 2014-05-20 11:44:00 | Kaila     | Spayed Female    |
| A410330   | Dog         | 2016-09-13 13:46:00 | Chewy     | Spayed Female    |

- Cookie는 보호소에 들어올 당시에 이미 중성화되어있었습니다.
- Maxwell 2는 보호소에 들어온 후 중성화되었습니다.
- Kaila는 보호소에 들어올 당시에 이미 중성화되어있었습니다.
- Chewy는 보호소에 들어온 후 중성화되었습니다.

따라서 SQL문을 실행하면 다음과 같이 나와야 합니다.

| ANIMAL_ID | ANIMAL_TYPE | NAME      |
| --------- | ----------- | --------- |
| A382192   | Dog         | Maxwell 2 |
| A410330   | Dog         | Chewy     |

---

## 문제 정보

| 난이도 | Lv. 3 |
| ------ | ----- |
| 정답률 | 85%   |

---

## 풀이

```SQL
SELECT AI.ANIMAL_ID, AI.ANIMAL_TYPE, AI.NAME
FROM ANIMAL_INS AS AI
JOIN ANIMAL_OUTS AS AO
    ON AI.ANIMAL_ID = AO.ANIMAL_ID
WHERE
    AI.SEX_UPON_INTAKE LIKE "Intact%" AND
    AO.SEX_UPON_OUTCOME NOT LIKE "Intact%"
ORDER BY AI.ANIMAL_ID;
```

---

## 결과

![결과](./assets/스크린샷%202025-08-01%2014.52.39.png)

---
