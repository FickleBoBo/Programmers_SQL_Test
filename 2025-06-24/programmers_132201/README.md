# [12세 이하인 여자 환자 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/132201)

## 문제 설명

다음은 종합병원에 등록된 환자정보를 담은 `PATIENT` 테이블입니다. `PATIENT` 테이블은 다음과 같으며 `PT_NO`, `PT_NAME`, `GEND_CD`, `AGE`, `TLNO`는 각각 환자번호, 환자이름, 성별코드, 나이, 전화번호를 의미합니다.

| Column name | Type        | Nullable |
| ----------- | ----------- | -------- |
| PT_NO       | VARCHAR(10) | FALSE    |
| PT_NAME     | VARCHAR(20) | FALSE    |
| GEND_CD     | VARCHAR(1)  | FALSE    |
| AGE         | INTEGER     | FALSE    |
| TLNO        | VARCHAR(50) | TRUE     |

## 문제

`PATIENT` 테이블에서 12세 이하인 여자환자의 환자이름, 환자번호, 성별코드, 나이, 전화번호를 조회하는 SQL문을 작성해주세요. 이때 전화번호가 없는 경우, 'NONE'으로 출력시켜 주시고 결과는 나이를 기준으로 내림차순 정렬하고, 나이 같다면 환자이름을 기준으로 오름차순 정렬해주세요.

## 예시

`PATIENT` 테이블이 다음과 같을 때

| PT_NO      | PT_NAME | GEND_CD | AGE | TLNO        |
| ---------- | ------- | ------- | --- | ----------- |
| PT22000003 | 브라운  | M       | 18  | 01031246641 |
| PT22000004 | 크롱    | M       | 7   | NULL        |
| PT22000006 | 뽀뽀    | W       | 8   | NULL        |
| PT22000009 | 한나    | W       | 12  | 01032323117 |
| PT22000012 | 뿡뿡이  | M       | 5   | NULL        |
| PT22000013 | 크리스  | M       | 30  | 01059341192 |
| PT22000014 | 토프    | W       | 22  | 01039458213 |
| PT22000018 | 안나    | W       | 11  | NULL        |
| PT22000019 | 바라    | W       | 10  | 01079068799 |
| PT22000021 | 릴로    | W       | 33  | 01023290767 |

SQL을 실행하면 다음과 같이 출력되어야 합니다.

| PT_NAME | PT_NO      | GEND_CD | AGE | TLNO        |
| ------- | ---------- | ------- | --- | ----------- |
| 한나    | PT22000009 | W       | 12  | 01032323117 |
| 안나    | PT22000018 | W       | 11  | NONE        |
| 바라    | PT22000019 | W       | 10  | 01079068799 |
| 뽀뽀    | PT22000006 | W       | 8   | NONE        |

---

## 문제 정보

| 난이도 | Lv. 1 |
| ------ | ----- |
| 정답률 | 90%   |

---

## 풀이

```SQL
SELECT
    PT_NAME,
    PT_NO,
    GEND_CD,
    AGE,
    IFNULL(TLNO, "NONE") AS TLNO
FROM PATIENT
WHERE AGE <= 12 AND GEND_CD = "W"
ORDER BY AGE DESC, PT_NAME;
```

---

## 결과

![결과](./assets/스크린샷%202025-06-24%2023.23.31.png)

---
