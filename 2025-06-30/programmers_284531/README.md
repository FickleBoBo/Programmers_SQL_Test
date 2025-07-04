# [노선별 평균 역 사이 거리 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/284531)

## 문제 설명

`SUBWAY_DISTANCE` 테이블은 서울지하철 2호선의 역 간 거리 정보를 담은 테이블입니다. `SUBWAY_DISTANCE` 테이블의 구조는 다음과 같으며 `LINE`, `NO`, `ROUTE`, `STATION_NAME`, `D_BETWEEN_DIST`, `D_CUMULATIVE`는 각각 호선, 순번, 노선, 역 이름, 역 사이 거리, 노선별 누계 거리를 의미합니다.

| Column name    | Type         | Nullable |
| -------------- | ------------ | -------- |
| LINE           | VARCHAR(10)  | FALSE    |
| NO             | NUMBER       | FALSE    |
| ROUTE          | VARCHAR(50)  | FALSE    |
| STATION_NAME   | VARCHAR(100) | FALSE    |
| D_BETWEEN_DIST | NUMBER       | FALSE    |
| D_CUMULATIVE   | NUMBER       | FALSE    |

## 문제

`SUBWAY_DISTANCE` 테이블에서 노선별로 노선, 총 누계 거리, 평균 역 사이 거리를 노선별로 조회하는 SQL문을 작성해주세요.

총 누계거리는 테이블 내 존재하는 역들의 `역 사이 거리`의 총 합을 뜻합니다. 총 누계 거리와 평균 역 사이 거리의 컬럼명은 각각 `TOTAL_DISTANCE`, `AVERAGE_DISTANCE`로 해주시고, 총 누계거리는 소수 둘째자리에서, 평균 역 사이 거리는 소수 셋째 자리에서 반올림 한 뒤 단위(km)를 함께 출력해주세요.

결과는 총 누계 거리를 기준으로 내림차순 정렬해주세요.

## 예시

`SUBWAY_DISTANCE` 테이블이 다음과 같을 때

| LINE  | NO  | ROUTE    | STATION_NAME     | D_BETWEEN_DIST | D_CUMULATIVE |
| ----- | --- | -------- | ---------------- | -------------- | ------------ |
| 2호선 | 45  | 성수지선 | 용답             | 2.3            | 51.1         |
| 2호선 | 46  | 성수지선 | 신답             | 1              | 52.1         |
| 2호선 | 47  | 성수지선 | 용두(동대문구청) | 0.9            | 53           |
| 2호선 | 48  | 성수지선 | 신설동           | 1.2            | 54.2         |
| 2호선 | 49  | 신정지선 | 도림천           | 1              | 55.2         |
| 2호선 | 50  | 신정지선 | 양천구청         | 1.7            | 56.9         |
| 2호선 | 51  | 신정지선 | 신정네거리       | 1.9            | 58.8         |
| 2호선 | 52  | 신정지선 | 까치산           | 1.4            | 60.2         |

SQL을 실행하면 다음과 같이 출력되어야 합니다.

| ROUTE    | TOTAL_DISTANCE | AVERAGE_DISTANCE |
| -------- | -------------- | ---------------- |
| 신정지선 | 6km            | 1.5km            |
| 성수지선 | 5.4km          | 1.35km           |

---

## 문제 정보

| 난이도 | Lv. 2 |
| ------ | ----- |
| 정답률 | 74%   |

---

## 풀이

```SQL
SELECT
    ROUTE,
    CONCAT(ROUND(SUM(D_BETWEEN_DIST), 1), "km") AS TOTAL_DISTANCE,
    CONCAT(ROUND(AVG(D_BETWEEN_DIST), 2), "km") AS AVERAGE_DISTANCE
FROM SUBWAY_DISTANCE
GROUP BY ROUTE
ORDER BY SUM(D_BETWEEN_DIST) DESC;
```

---

## 결과

| 채점 결과        |
| ---------------- |
| 테스트 1 〉 통과 |

---
