# WITH 절
> SQL의 함수 중 하나인  `WITH절` 의 사용방법과 사용예시를 알아보자

## 사용하는 경우
서브쿼리가 길거나 삼중조인이 필요한 상황 등 쿼리가 너무 길어지게 되는 경우 `WITH` 이하 절로 서브쿼리를 따로 분리하기 위해 사용한다.

## 예시
[프로그래머스 - 저자별 카테고리별 매출액 집계하기](https://school.programmers.co.kr/learn/courses/30/lessons/144856)
<br>
한 서점에서 판매중인 도서 정보를 담은 `BOOK` 테이블과 저자 정보를 담은 `AUTHOR` 테이블, 각 도서의 날짜별 판매량 정보를 담은 `BOOK_SALES` 테이블이 존재한다.
이 때 `2022년 1월`의 도서 판매 데이터를 기준으로 저자별, 카테고리별 매출액 (`TOTAL_SALES = 판매량 * 판매가`)을 구하여, 저자 ID(`AUTHOR_ID`), 저자명(`AUTHOR_NAME`), 카테고리(`CATEGORY`), 매출액(`SALES`) 리스트를 출력하는 SQL문을 구하자.

- WITH 절을 알기전 (애송이 시절)
```sql
SELECT A.AUTHOR_ID, A.AUTHOR_NAME, B.CATEGORY, SUM(S.SALES * B.PRICE) AS TOTAL_SALES
FROM AUTHOR A, BOOK B, BOOK_SALES S
WHERE A.AUTHOR_ID = B.AUTHOR_ID
AND B.BOOK_ID = S.BOOK_ID
AND TO_CHAR(S.SALES_DATE, 'YYYYMM') = '202201'
GROUP BY A.AUTHOR_ID, A.AUTHOR_NAME, B.CATEGORY
ORDER BY A.AUTHOR_ID ASC, B.CATEGORY DESC
```
테이블 3개를 전부 조인하여 삼중조인을 만들었다.

- WITH 절을 활용한 결과
```SQL
WITH EX AS 
(
 SELECT B.BOOK_ID AS BOOK_ID, B.AUTHOR_ID AS AUTHOR_ID, A.AUTHOR_NAME AS AUTHOR_NAME, B.CATEGORY AS CATEGORY, B.PRICE AS PRICE
 FROM AUTHOR A, BOOK B 
 WHERE A.AUTHOR_ID = B.AUTHOR_ID (+)
)
SELECT E.AUTHOR_ID AS AUTHOR_ID, 
       E.AUTHOR_NAME AS AUTHOR_NAME,
       E.CATEGORY AS CATEGORY,
       SUM( S.SALES * E.PRICE) AS TOTAL_SALES
FROM EX E, BOOK_SALES S
WHERE E.BOOK_ID = S.BOOK_ID 
AND TO_CHAR(SALES_DATE, 'YYYYMM') = '202201'
GROUP BY AUTHOR_ID, AUTHOR_NAME, CATEGORY
ORDER BY AUTHOR_ID ASC, CATEGORY DESC
```

`AUTHOR` 테이블과 `BOOK` 테이블을 OUTER JOIN한 서브쿼리를 만들어 `EX` 로 별칭한 후, 별칭한 `EX` 테이블과 `BOOK_SALES` 테이블을 INNER JOIN하여 결과값을 출력하였다.

> 이 경우는 WITH절을 사용했을 때의 쿼리가 쓰지 않았을 때의 쿼리보다 더 길어졌기 때문에 사실 굳이 WITH절을 사용할 필요는 없지만, 해당 서브쿼리를 계속해서 불러와야 하는 경우 WITH절이 훨씬 편리하다.