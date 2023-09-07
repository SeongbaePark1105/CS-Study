# SQL 활용

### 1. 조인

#### ① EQUI(등가) JOIN(교집합)

1. ##### EQUI JOIN

   - 조인은 여러 개의 릴레이션을 사용해서 새로운 릴레이션을 만드는 과정

   - 조인의 가장 기본은 교집합을 만드는 것

   - 두 개의 테이블 간에 일치하는 것을 조인함

     ```sql
     SELECT * FROM EMP, DEPT
     WHERE EMP.NO == DEPT.NO;
     ```

     - <b>EQUI JOIN</b>은 <b>=</b>을 사용해서 두 개의 테이블을 연결
     - <b>WHERE</b>절에 추가 조건 및 정렬을 할 수 있음

2. ##### INNER JOIN

   - <b>ON</b>문을 사용해서 테이블을 연결

     ```sql
     SELECT * FROM EMP INNER JOIN DEPT
     ON EMP.NO = DEPT.NO;
     ```

     - 마찬가지로 <b>ON</b>절에 추가 조건 및 정렬을 할 수 있음

3. ##### HASH JOIN

   - 먼저 선행 테이블을 결정하고 선행 테이블에서 주어진 조건(Where구)에 해당하는 행을 선택
   - 해당 행이 선택되면 조인 키를 기준으로 해시 함수를 사용해서 해시 테이블을 메인 메모리에 생성하고 후행 테이블에서 주어진 조건에 만족하는 행을 찾음
   - 후행 테이블의 조인 키를 사용해서 해시 함수를 적용하여 해당 버킷을 검색

4. ##### INTERSECT 연산

   - 두 개의 테이블에서 교집합을 조회
   - 즉, 두 개 테이블에서 공통된 값을 조회

#### ② Non-EQUI(비등가) JOIN

- 두 개의 테이블 간에 조인하는 경우 <b>=</b>을 사용하지 않고 <b>>, <. >=, <=</b>등을 사용함
- 즉, 정확하게 일치하지 않는 것을 조회하는 것

#### ③ OUTER JOIN

- 두 개의 테이블 간에 교집합을 조회하고 한쪽 테이블에만 있는 데이터도 포함시켜서 조회함
- 예를 들면 <b>DEPT 테이블</b>과 <b>EMP 테이블</b>을 <b>OUTER JOIN</b>하면 <b>DEPTNO</b>가 같은 것을 조회하고 <b>DEPT 테이블</b>에만 있는 <b>DEPTNO</b>도 포함시킴
- 이때 왼쪽 테이블에만 있는 행도 포함하면 <b>LEFT OUTER JOIN</b>
- 오른쪽 테이블의 행만 포함시키면 <b>RIGHT OUTER JOIN</b>
- <b>FULL OUTER JOIN</b>은 <b>LEFT OUTER JOIN</b>과 <b>RIGHT OUTER JOIN</b> 모두를 하는 것
- Oracle 데이터베이스에서는 <b>OUTER JOIN</b>을 할 때 <b>+</b>기호를 사용해서 할 수 있음

#### ④ CROSS JOIN

- 조인 조건구 없이 2개의 테이블을 하나로 조인
- 조인구가 없기 때문에 카테시안 곱이 발생함
- 예를 들어 행이 14개와 행이 4개인 테이블을 조인하면 56개의 행이 조회됨
- FROM절에 <b>CROSS JOIN</b>구를 사용하면 됨

#### ⑤ UNION을 이용한 합집합 구현

1. ##### UNION

   - 두 개의 테이블을 하나로 만드는 연산

   - 주의사항은 두 개의 <b>테이블의 칼럼 수</b>, <b>칼럼의 데이터 형식</b> 모두가 일치해야 함

   - 두 개의 테이블을 하나로 합치면서 <b>중복된 데이터를 제거</b>

   - 그래서 <b>UNION</b>은 <b>정렬</b>과정을 발생시킴

2. ##### UNION ALL

   - 두 개의 테이블을 하나로 합치는 것
   - 중복을 제거하거나 정렬을 유발하지 않음
   - 즉, 중복 허용!

#### ⑥ 차집합을 만드는 MINUS

- 두 개의 테이블에서 차집합을 조회

- 즉, 먼저 쓴 <b>SELECT문</b>에는 있고 뒤에 쓰는 <b>SELECT문</b>에는 없는 집합을 조회

- <b>MS-SQL</b>에서는 <b>MINUS</b>와 동일한 연산이 <b>EXCEPT</b>임

  ```sql
  SELECT DEPTNO FROM DEPT (10, 20, 30, 40)
  MINUS
  SELCET DEPTNO FROM EMP; (10, 20, 30)
  ```

  - 각 테이블이 위와 같은 값을 가지고 있을 때 결과 값은 40만 출력됨



### 2. 계층형 조회 (CONNECT BY)

- <b>CONNECT BY</b>는 트리 형태의 구조로 질의를 수행하는 것으로 <b>START WITH</b>구는 시작 조건을 의미하고 <b>CONNECT BY PRIOR</b>는 조인 조건임

- Root 노드로부터 하위 노드의 질의를 실행함

- 계층형 조회에서 <b>MAX(LEVEL)</b>을 사용하여 최대 계층 수를 구할 수 있음

- 즉, 계층형 구조에서 마지막 <b>Leaf Node</b>의 계층값을 구함

  ```sql
  SELECT MAX(LEVEL)
  FROM Limbest.EMP
  START WITH MGR IS NULL
  CONNECT BY PRIOR EMPNO = MRG;
  ```

- 계층형 조회 결과를 명확히 보기 위해서 <b>LPAD</b>함수를 사용

  ```
  SELECT LEVEL, LPAD(' ', 4*(LEVEL - 1))
  ```

  - 값 만큼 공백을 주어서 트리 형태로 보기 위해서 사용 됨

##### ▶CONNECT BY 키워드

- ##### LEVEL

  - 검색 항목의 깊이를 의미
  - 즉, 계층구조에서 가장 상위 레벨이 1이 됨(루트)

- ##### CONNECT_BY_ROOT

  - 계층 구조에서 가장 최상위 값을 표시

- ##### CONNECT_BY_ISLEAF

  - 계층 구조에서 가장 최하위를 표시

- ##### SYS_CONNECT_BY_PATH

  - 계층 구조의 전체 전개 경로를 표시

- ##### NOCYCLE

  - 순환 구조가 발생지점까지만 전개

- ##### CONNECT_BY_ISCYCLE

  - 순환 구조 발생 지점을 표시

- <b>CONNECT BY</b>구는 순방향 조회와 역방향 조회가 있음

- ##### 순방향 조회

  - 부모 엔터티로부터 자식 엔터티을 찾아가는 검색을 의미

- ##### 역방향 조회

  - 자식 엔터티로부터 부모 엔터티를 찾아가는 검색

##### ▶계층형 조회

- ##### START WIHT 조건

  - 계층 전개의 시작 위치를 지정하는 것

- ##### PRIOR 자식 = 부모

  - 부모에서 자식방향으로 검색을 수행하는 순방향 전개

- ##### PRIOR 부모 = 자식

  - 자식에서 부모방향으로 검색을 수행하는 역방향 전개

- ##### NOCYCLE

  - 데이터를 전개하면서 이미 조회된 데이터를 다시 조회되면 <b>CYCLE</b>이 형성됨
  - 이때 <b>NOCYCLE</b>은 사이클이 발생되지 않게 함

- ##### Order siblings by 칼럼명

  - 동일한 LEVEL인 형제노드 사이에서 정렬을 수행



### 3. 서브쿼리(Subquery)

#### ① Main query와 Subquery

- <b>subquery</b>는 <b>SELECT문</b> 내에 다시 <b>SELECT</b>문을 사용하는 SQL문

- ##### 인라인 뷰

  - <b>FROM</b>구에 <b>SELECT</b>문을 사용

- ##### 스칼라 서브쿼리

  - <b>SELECT</b>문에 <b>Subquery</b>를 사용

- ##### 서브쿼리

  - <b>WHERE</b>구에 <b>SELECT</b>문을 사용

- ##### 메인쿼리

  - 서브쿼리 밖에 있는 <b>SELECT</b>문

- 인라인 뷰를 사용하면 가상의 테이블을 만드는 효과를 얻을 수 있음

#### ② 단일 행 서브쿼리와 다중 행 서브쿼리

- 서브쿼리는 반환하는 행 수가 한 개인 것과 여러 개인 것에 따라서 <b>단일 행 서브쿼리</b>와 <b>멀티 행 서브쿼리</b>로 분류됨

- ##### 단일 행 서브쿼리

  - 하나의 행만 반환하는 서브쿼리로 비교 연산자를 사용함

- ##### 다중 행 서브쿼리

  - 여러 개의 행을 반환하는 것

  - ##### IN, ANY, ALL, EXISTS를 사용

#### ③ 다중 행 Subquery

- 다중 행 연산자를 사용해야 함
- 서브쿼리 결과가 여러 개의 행을 반환하는 것

##### ▶다중 행 비교 연산자

- ##### IN

  - <b>Main query</b> 비교조건이 <b>SubQuery</b>의 결과중 하나만 동일하면 참<b>(OR조건)</b>

- ##### ALL

  - <b>Main query</b>의 <b>Subquery</b>의 결과가 모두 동일하면 참

  - ##### < ALL

    - 최솟값을 반환

  - ##### > ALL

    - 최댓값을 반환

- ##### ANY

  - <b>Main query</b>의 비교조건이 <b>Subquery</b>의 결과 중 하나 이상 동일하면 참

  - ##### < ANY

    - 하나라도 크게 되면 참

  - ##### > ANY

    - 하나라도 작게 되면 참

- ##### EXISTS

  - <b>Main query</b>와 <b>Subquery</b>의 결과가 하나라도 존재하면 참

#### ④ 스칼라 Subquery

- 반드시 한 행과 한 칼럼만 반환하는 서브쿼리

- 만약 여러 행이 반환되면 오류가 발생됨

  ```sql
  SELECT ENAME, (SELECT AVG(SAL) FROM EMP) as '급여' FROM EMP;
  ```

#### ⑤ 연관 Subquery

- 연관 Subquery는 Subquery 내에서 <b>Main query</b> 내의 칼럼을 사용하는 것을 의미

  ```sql
  SELECT *
  FROM EMP a
  WHERE a.NO = 
  		(SELECT NO FROM DEPT b
  		  WHERE b.NO = a.NO);
  ```



### 4. 그룹 함수

#### ① ROLLUP

- <b>GROUP BY</b>의 칼럼에 대해서 <b>Subtotal</b>을 만들어줌

- <b>ROLLUP</b>을 할 때 <b>GROUP BY</b>구에 칼럼이 두 개 이상 오면 순서에 따라서 결과가 달라짐

  ```sql
  SELECT empno, ename, SUM(num) 
  FROM emp
  GROUP BY ROLLUP(empno);
  ```

  - <b>empno</b>기준으로 합계를 출력하고 마지막에 전체 합계를 출력함

  ```sql
  SELECT empno, ename, SUM(num) 
  FROM emp
  GROUP BY ROLLUP(empno, ename);
  ```

  - <b>empno</b>와 <b>ename</b> 기준으로 묶어서 합계를 출력하고 <b>empno</b>를 기준 합계를 출력함
  - 마지막으로 전체 <b>empno</b>기준 전쳬 합계를 출력함

#### ② GROUPING 함수

- <b>ROLLUP, CUBE, GROUPING SETS</b>에서 생성되는 합계값을 구분하기 위해서 만들어진 함수
- 예를 들어 소계, 합계 등이 계산되면 <b>GROUPING</b> 함수는 <b>1</b>을 반환하고 그렇지 않으면 <b>0</b>을 반환해서 합계값을 식별
- 함수의 기능을 사용하면 사용자가 필요로 하는 데이터를 SELECT문으로 작성하여 제공할 수 있음

#### ③ GROUPING SETS 함수

- GROUP BY에 나오는 칼럼의 순서와 관계없이 다양한 소계를 만들 수 있음

- GROUP BY에 나오는 칼럼의 순서와 관계없이 개별적으로 모두 처리

  ```sql
  SELECT DEPTNO, JOB, SUM(SAL)
  FROM EMP
  GROUP BY GROUPING SETS(DEPTNO, JOB);
  ```

  - <b>직업별 합계(JOB)</b>와 <b>부서별 합계(DEPTNO)</b> 가 개별적으로 조회됨

#### ④ CUBE 함수

- CUBE 함수에 제시한 칼럼에 대해서 결합 가능한 모든 집계를 계산
- 다차원 집계를 제공하여 다양하게 데이터를 분석할 수 있게 됨
- 예를 들어 부서와 직업을 <b>CUBE</b>로 사용하면 <b>부서별 합계, 직업별 합계, 부서별 직업별 합계, 전체합계</b>가 조회 됨
- 즉, 조합할 수 있는 경우의 수가 모두 조합되는 것



### 5. 윈도우 함수

#### ① 윈도우 함수

- 행과 행 간의 관계를 정의하기 위해서 제공되는 함수

- 원도우 함수를 사용해서 순위, 합계, 평균, 행 위치 등을 조작할 수 있음

  ```sql
  SELECT WINDOW_FUNCTION(ARGUMENTS)
  	OVER (PARTITION BY 칼럼
  			ORDER BY WINDOWING절)
  FROM 테이블명;
  ```

##### ▶윈도우 함수 구조

- ##### ARGUMENTS(인수)

  - 윈도우 함수에 따라서 0~N개의 인수를 설정

- ##### PARTITION BY

  - 전체 집합을 기준에 의해 소그룹으로 나눔

- ##### ORDER BY

  - 어떤 항목에 대해서 정렬함

- ##### WINDOWING

  - 행 기준의 범위를 정함
  - <b>ROWS</b>는 <b>물리적 결과의 행 수</b>이고 <b>RANGE</b> 는 <b>논리적인 값에 의한 범위</b>

##### ▶WINDOWING

- ##### ROWS

  - 부분집합인 윈도우 크기를 물리적 단위로 행의 집합을 지정

- ##### RANGE

  - 논리적인 주소에 의해 행 집합을 지정

- ##### BETWEEN ~ AND

  - 윈도우의 시작과 끝의 위치를 지정

- ##### UNBOUNDED PRECEDING

  - 윈도우의 시작 위치가 첫 번째 행임을 의미

- ##### UNBOUNDED FOLLOWING

  - 윈도우 마짐가 위치가 마지막 행임을 의미

- ##### CURRENT ROW

  - 윈도우 시작 위치가 현재 행임을 의미

```sql
SELECT EMPNO,ENAME,SAL,
SUM(SAL) OVER(ORDER BY SAL
				ROWS BETWEEN UNBOUNDED PRECEDING
				AND UNBOUNDED FOLLOWING) AS TOT SAL
FROM EMP;
```

- <b>TOTASL</b>에 처음부터 마지막까지의 합계를 계산
- 즉, 전체합계임 모든 행이

```sql
SELECT EMPNO,ENAME,SAL,
SUM(SAL) OVER(ORDER BY SAL
				ROWS BETWEEN UNBOUNDED PRECEDING
				AND CURRENT ROW) AS TOT SAL
FROM EMP;
```

- 처음부터 현재행까지의 합계를 계산
- 그러므로 각 행마다 누적 합계를 구하는 것

#### ② 순위 함수

- 윈도우 함수는 특정 항목과 파티션에 대해서 순위를 게산할 수 있는 함수를 제공

##### ▶순위 관련 윈도우 함수

- ##### RANK

  - 특정항목 및 파티션에 대해서 순위를 계산

  - ##### 동일한 순위는 동일한 값이 부여

  - 예를 들어, 1등이 2명이면 <b>1, 1, 3, 4...</b>으로 순위가 부여됨

    - 2등이 없어지는거임

- ##### DENSE_RANK

  - ##### 동일한 순위를 하나의 건수로 계산

    - 건수로 계산하기 때문에 1등이 2명이여도 <b>1, 2, 3, 4...</b>으로 순위가 부여됨

- ##### ROW_NUMBER

  - 동일한 순위에 대해서 <b>고유의 순위를 부여</b>
  - 값이 같아도 <b>1, 2, 3, 4...</b>으로 순위가 부여됨

#### ③ 집계 함수

- 윈도우 함수를 제공

- ##### SUM, AVG, COUNT, MAX와 MIN

#### ④ 행 순서 관련 함수

- 행 순서 관련 함수는 <b>상위 행의 값을 하위에 출력</b>하거나 <b>하위 행의 값을 상위 행에 출력</b>할 수 있음

##### ▶행 순서 관련 윈도우 함수

- ##### FIRST_VALUE

  - 파티션에서 <b>가장 처음에 나오는 값</b>을 구함
  - <b>MIN 함수</b>를 사용해서 같은 결과를 구할 수 있음

- ##### LAST_VALUE

  - 파티션에서 <b>가장 나중에 나오는 값</b>을 구함
  - <b>MAX 함수</b>를 사용해서 같은 결과를 구할 수 있음

- ##### LAG

  - <b>이전 행</b>을 가지고 옴

- ##### LEAD

  - 윈도우에서 <b>특정 위치의 행을 가지고 옴</b>

    - 즉, 현재 행의서 N번째 아래에 있는 값을 가져옴
    - 여기서 N이란 <b>LEAD</b>함수에 쓰인 값

  - 기본값은 <b>1</b>

  - ##### LEAD(칼럼명, 값)

#### ⑤ 비율 관련 함수

##### ▶비율 관련 윈도우 함수

- ##### CUME_DIST

  - 파티션 전체 건수에서 현재 행보다 작거나 같은 건수에 대한 누적 백분율을 조회
  - 누적 분포상에 위치를 0~1 사이의 값을 가짐

- ##### PERCENT_RANK

  - 파티션에서 제일 먼저 나온 것을 0으로 제일 늦게 나온 것을 1로하여 값이 아닌 행의 순서별 백분율을 조회

- ##### NTILE

  - 파티션별로 전체 건수를 <b>ARGUMENT</b> 값으로 N 등분한 결과를 조회

- #####  RATIO_TO_REPORT

  - 파티션 내에 전체 SUM(칼럼)에 대한 행 별 칼럼값의 백분율을 소수점까지 조회



### 6. 테이블 파티션

#### ① 파티션 기능

- 대용량의 테이블을 여러 개의데이터 파일에 분리해서 저장
- 테이블의 데이터가  물리적으로 분리된 데이터 파일에 저장되면 <b>입력, 수정, 삭제, 조회</b> 성능 향상
- 파티션을 각각의 파티션 별로 독립적으로 관리될 수 있음
  - 즉, 파티션 별로 백업하고 복구가 가능하면 파티션 전용 인덱스 생성도 가능
- 파티션은 Oracle 데이터베이스의 논리적 관리 단위인 테이블 스페이스 간에 이동이 가능
- 데이터를 조회할 대 데이터의 범위를 줄여서 성능이 향상

#### ② Range Partition

- 테이블의 칼럼 중에서 값의 범위를 기준으로 여러 개의 파티션으로 데이터를 나누어 저장하는 것
- 예를 들어, 값의 범위가 1000~ 3000 / 4000~ 5000 기준으로 데이터를 저장

#### ③ List Partition

- 특정 값을 기준으로 분할
- 예를 들어 값이 10인것은 1파티션 20인것은 2파티션 이런 느낌

#### ④ Hash Partition

- 데이터베이스 관리 시스템이 내부적으로 해시 함수를 사용해서 데이터를 분할
- 결과적으로 데이터베이스 관리 시스템이 알아서 분할하고 관리하는 것
- <b>Hash Partition</b>이외에도 <b>Composite Partition</b>이 있는데 이것은 여러 개의 파티션 기법을 조합해서 사용하는 것

#### ⑤ 파티션 인덱스

- 파티션 키를 사용해서 인덱스를 만드는 <b>Prefixed Index</b>와 해당 파티션만 사용하는 <b>Local Index</b>등으로 나뉨
- Oracle 데이터베이스는 <b>Global Non-Prefixed</b>를 지원하지 않음

##### ▶파티션 인덱스 구분

- ##### Global Index

  - 여러 개의 파티션에서 하나의 인덱스를 사용(전역)

- ##### Local Index

  - 해당 파티션 별로 각자의 인덱스를 사용(지역)

- ##### Prefixed Index

  - 파티션 키와 인덱스 키가 동일

- ##### Non Prefixed Index

  - 파티션 키와 인덱스 키가 다르다
