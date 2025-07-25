# 코딩테스트 SQL 문법

## SQL 쿼리 순서

### 적는 순서

```
1. SELECT 컬럼
2. FROM 테이블
3. JOIN 다른 테이블 ON 조건
4. WHERE 조건
5. GROUP BY 컬럼
6. HAVING 조건
7. ORDER BY 정렬 조건
8. LIMIT 개수
```

### 실행 순서

```
1. FROM
2. JOIN
3. WHERE
4. GROUP BY
5. HAVING
6. SELECT
7. ORDER BY
8. LIMIT
```

---

## SQL JOIN

<img src="./assets/join.png" width="100%"/>

---

## 연산자

### [산술 연산자](https://dev.mysql.com/doc/refman/8.4/en/non-typed-operators.html)

- `+`
- `-`
- `*`
- `/`
- `%`
- `&`
- `|`
- `~`

### [비교 연산자](https://dev.mysql.com/doc/refman/8.4/en/comparison-operators.html)

- `=`
- `!=`, `<>`
- `>`
- `<`
- `>=`
- `<=`

### [논리 연산자](https://dev.mysql.com/doc/refman/8.4/en/logical-operators.html)

- `AND`
- `OR`
- `NOT`

### [`expr BETWEEN min AND max`](https://dev.mysql.com/doc/refman/8.4/en/comparison-operators.html#operator_between)

- `min <= expr AND expr <= max`와 동일하며 조건을 만족하면 1, 아니면 0 반환

### [`IS NULL`](https://dev.mysql.com/doc/refman/8.4/en/comparison-operators.html#operator_is-null), [`IS NOT NULL`](https://dev.mysql.com/doc/refman/8.4/en/comparison-operators.html#operator_is-not-null)

- `NULL` 여부에 대한 비교에서 사용하며 조건을 만족하면 1, 아니면 0 반환

### [`ISNULL(expr)`](https://dev.mysql.com/doc/refman/8.4/en/comparison-operators.html#function_isnull)

- `expr`이 `NULL`이면 1, 아니면 0 반환

### [`expr LIKE Pattern`](https://dev.mysql.com/doc/refman/8.4/en/string-comparison-functions.html#operator_like)

- `expr`과 `Pattern`에 대한 패턴 매칭이 되면 1, 아니면 0 반환

### `LIKE` 연산자 와일드 카드

- `_` -> 1개의 문자
- `%` -> 0개 이상의 문자

```SQL
"test_"
"_test"
"_test_"
"test%"
"%test"
"%test%"
```

### [`expr IN (value, ...)`](https://dev.mysql.com/doc/refman/8.4/en/comparison-operators.html#operator_in)

- `expr`에 대해 리스트에 일치하는 값이 있으면 1, 아니면 0 반환
- 서브쿼리에 대해서도 사용 가능

---

## 날짜/시간

### 데이터 타입

- `DATE`
  - 날짜만 저장(YYYY-MM-DD)
- `DATETIME`
  - 날짜와 시간 저장(YYYY-MM-DD HH:MM:SS)

### 함수

- [`YEAR(expr)`](https://dev.mysql.com/doc/refman/8.4/en/date-and-time-functions.html#function_year)
  - `expr`에서 연도 추출
- [`MONTH(expr)`](https://dev.mysql.com/doc/refman/8.4/en/date-and-time-functions.html#function_month)
  - `expr`에서 월 추출
- [`DAY(expr)`](https://dev.mysql.com/doc/refman/8.4/en/date-and-time-functions.html#function_day)
  - `expr`에서 일 추출
- [`HOUR(expr)`](https://dev.mysql.com/doc/refman/8.4/en/date-and-time-functions.html#function_hour)
  - `expr`에서 시 추출
- [`MINUTE(expr)`](https://dev.mysql.com/doc/refman/8.4/en/date-and-time-functions.html#function_minute)
  - `expr`에서 분 추출
- [`SECOND(expr)`](https://dev.mysql.com/doc/refman/8.4/en/date-and-time-functions.html#function_second)
  - `expr`에서 초 추출
- [`QUARTER(expr)`](https://dev.mysql.com/doc/refman/8.4/en/date-and-time-functions.html#function_quarter)
  - `expr`에서 분기 추출
- [`DATE_FORMAT(expr, format)`](https://dev.mysql.com/doc/refman/8.4/en/date-and-time-functions.html#function_date-format)
  - `expr`을 `format`으로 포맷팅
  - `%Y`
    - 4자리 연도
  - `%m`
    - 2자리 월
  - `%d`
    - 일
  - `%H`
    - 시
  - `%i`
    - 분
  - `%s`
    - 초
- [`DATEDIFF(date1, date2)`](https://dev.mysql.com/doc/refman/8.4/en/date-and-time-functions.html#function_datediff)
  - 두 날짜의 차 반환(date1 - date2)

---

## 문자열

### 함수

- [`LEFT(str, n)`](https://dev.mysql.com/doc/refman/8.4/en/string-functions.html#function_left)
  - 왼쪽부터 n개 문자
- [`RIGHT(str, n)`](https://dev.mysql.com/doc/refman/8.4/en/string-functions.html#function_right)
  - 오른쪽부터 n개 문자
- [`CONCAT(str1, str2, ...)`](https://dev.mysql.com/doc/refman/8.4/en/string-functions.html#function_concat)
  - 여러 문자열을 합침

---

## 숫자

### 함수

- [`ROUND(num, digit)`](https://dev.mysql.com/doc/refman/8.4/en/mathematical-functions.html#function_round)
  - digit에서 num 반올림(생략시 0)
