# SQL 기본

### 1. 관계형 데이터베이스

#### ① 관계형 데이터베이스

1. ##### 관계형 데이터베이스의 등장

   - 릴레이션과 릴레이션의 조인 연산을 통해서 합집합, 교집합, 차집합 등을 만들 수 있음

2. ##### 데이터베이스와 데이터베이스 관리 시스템의 차이점

   - 종류는 <b>계층형, 네트워크형 데이터베이스, 관계형 데이터베이스</b>가 있음

   - ##### 계층형 데이터베이스

     - <b>트리</b>형태의 자료구조에 데이터를 저장하고 관리
     - <b>1 : N</b> 관계 (부모와 자식으로 볼 수 있음0)

   - ##### 네트워크 데이터베이스

     - <b>오너</b>와 <b>멤버</b>형태로 데이터를 저장
     - <b>1 : N</b>과 함께 <b>M : N</b>도 표현이 가능

   - ##### 관계형 데이터베이스

     - 릴레이션에 데이터를 저장하고 관리
     - 릴레이션을 사용해서 <b>집합 연산</b>과 <b>관계 연산</b>을 할 수 있음

3. ##### 관계형 데이터베이스 집합 연산과 관계 연산

   - ##### 집합 연산

     - ##### 합집합 (Union)

       - 두 개의 릴레이션을 하나로 합치는 것
       - 중복된 행(튜플)은 하나만 조회

     - ##### 차집합 (Difference)

       - 본래 릴레이션에는 존재하고 다른 릴레이션에는 존재하지 않는 것을 조회

     - ##### 교집합 (Intersection)

       - 두 개의 릴레이션 간에 공통된 것을 조회

     - ##### 곱집합 (Cartesian product)

       - 각 릴레이션에 존재하는 모든 데이터를 조합하여 연산

   - ##### 관계 연산

     - ##### 선택 연산 (Selection)

       - 릴레이션에서 조건에 맞는 행(튜플)만을 조회

     - ##### 투영 연산 (Projection)

       - 릴레이션에서 조건에 맞는 속성만을 조회

     - ##### 결합 연산 (Join)

       - 여러 릴레이션의 공통된 속성을 사용해서 새로운 릴레이션을 만듬

     - ##### 나누기 연산 (Division)

       - 중복된 행을 제거하는 연산

#### ② 테이블 구조

- <b>기본키</b>는 하나의 테이블에서 <b>유일성</b>과 <b>최소성</b>, <b>Not Null</b>을 만족하면서 해당 테이블을 대표

- 행과 칼럼으로 구성

- ##### 행 (Row)

  - 하나의 테이블에 저장되는 값으로 <b>튜플</b>이라고도 함

- ##### 칼럼 (Column)

  - 어떤 데이터를 저장하기 위한 필드로 <b>속성</b>이라고도 함

- ##### 외래키 (Foreign key)

  - 다른 테이블의 기본키를 참조(조인)하는 칼럼
  - 관계 연산 중에서 <b>결합 연산(Join)</b>을 하기 위해서 사용



### 2. SQL 종류

#### ① SQL (Structured Query Language)

- SQL은 관계형 데이터베이스에 대해서 데이터의 구조를 <b>정의, 데이터 조작, 데이터 제어</b>등을 할 수 있는 <b>절차형 + 비절차형</b> 언어임

#### ② SQL의 종류

1. ##### SQL의 종류

   - ##### DDL (Data Definition Language)

     - 관계형 데이터베이스의 구조를 정의하는 언어

     - ##### CREATE, ALTER, DROP, RENAME, TRUNCATE

   - ##### DML (Data Manipulation Language)

     - 테이블에서 데이터를 <b>입력, 수정, 삭제, 조회</b>

     - 즉, 데이터 조작

     - ##### INSERT, UPDATE, DELETE, SELECT

   - ##### DCL (Data Control Language)

     - 데이터베이스 사용자에게 권한을 부여하거나 회수

     - ##### GRANT, REVOKE

   - ##### TCL (Transaction Control Language)

     - 트랜젝션을 제어하는 명령어

     - ##### COMMIT, ROLLBACK, SAVEPOINT

   - 작업의 순서는 <b>DCL -> DDL -> DML</b>

2. ##### 트랜젝션 (Transaction)

   - 데이터베이스의 작업을 처리하는 단위

   - ##### 트랜잭션 특성

     - ##### 원자성 (Atomicity)

       - 데이터베이스 연산의 전부가 실행되거나 전혀 실행되지 않아야 함 

       - ##### All or Nothing

     - ##### 일관성 (Consistency)

       - 트랜잭션 실행 결과로 데이터베이스의 상태가 모순되지 않아야 함
       - 트랜잭션 실행 후에도 일관성이 유지되어야 함

     - ##### 고립성 (Isolation)

       - 트랜잭션 실행 중에 생성하는 연산의 중간결과는 다른 트랜잭션이 접근할 수 없음
       - 즉, 부분적인 실행 결과를 다른 트랜잭션이 볼 수 없음

     - ##### 영속성 (Durability)

       - 실행을 성공적으로 완료하면 그 결과는 영구적 보상이 되어야 함

#### ③ SQL문의 실행 순서

- SQL문은 <b>DDL, DML, DCL</b> 3단계를 걸쳐서 실행 됨
- SQL 실행 순서는 <b>파싱 -> 실행 -> 인출



### 3. DDL (Data Definition Language)

#### ① 테이블 생성

- <b>Create Table</b>문을 사용하여 테이블 생성

  - 테이블을 생성할 때 기본키, 외래키, 제약사항 등을 설정할 수 있음

- <b>Alter Table</b>문을 사용하여 테이블 변경

  - 생성된 테이블을 변경
  - 칼럼을 추가하거나 변경, 삭제 가능
  - 기본키를 설정하거나, 외래키를 설정

- <b>Drop Table</b>문을 사용하여 테이블 삭제

  - 테이블의 데이터 구조뿐만 아니라 저장된 데이터도 모두 삭제

    ```sql
    CREATE TABLE EMP(
    	empno bigint(10),
    	ename VARCHAR(20),
    	CONSTRAINT emppk PRIMARY KEY (empno)
        // CONSTRAINT emppk PRIMARY KEY (empno, ename) 기본 키를 두개로 설정할 수 도 있음
    );
    ```

    

- ##### 외래키 설정법

  ```sql
  constraint deptkf(외래키이름) foreign key(deptno)<-참조 받아서 생성 될 테이블의 칼럼
  references dept(deptno) <- dept 테이블의 deptno 칼럼을 참조한다는 의미
  즉,
  constraint 외래키이름 foreign key(참조 받을 테이블의 칼럼명)
  references 참조되는 테이블명(참조되는 테이블의 칼럼 명)
  ```

3. ##### 테이블 생성 시 CASECADE 사용

   - CASECADE 옵션은 참조 관계(기본키와 외래키 관계)가 있을 경우 참조되는 데이터를 자동으로 반영할 수 있음
   - 즉, 값이 변경되면 변경되고 삭제되면 같이 삭제됨

   ```sql
   constraint deptkf foreign key(deptno)
   references dept(deptno)
   on delete CASECADE
   EMP 테이블임
   ```

   - 참조하고 있는 테이블(DEPT)의 데이터가 삭제되면 자동으로 자신(EMP)도 삭제되는 옵션
   - 해당 기능을 사용하면 참조 무결성을 준수 할 수 있음

#### ② 테이블 변경

- <b>ALTER TABLE</b>문을 통해 테이블 변경을 할 수 있음
- 테이블명 변경, 칼럼 추가, 변경, 삭제 등을 할 수 있음

1. ##### 테이블명 변경

   ```sql
   ALTER TABLE EMP(기존 테이블명)
   	RENAME TO NEW_EMP(새로운 테이블 명);
   ```

2. #####  칼럼 추가

   ```sql
   ALTER TABLE EMP
   	ADD (age number(2) default 1) <- (칼럼 작성);
   ```

3. ##### 칼럼 변경

   - 데이터 타입을 변경하거나 데이터의 길으를 변경할 수 있음
   - 칼럼을 변경할 때 제약조건을 다시 설정할 수 있음
   - 칼럼의 데이터 타입을 변경할 때 기존 데이터가 있는 경우 에러가 발생

   ```sql
   ALTER TABLE EMP
   	MODIFY (ename varchr2(40) not null);
   ```

4. ##### 칼럼 삭제

   ```sql
   ALTER TABLE EMP
   	DROP COLUMN age;
   ```

5. ##### 칼럼명 변경

   ```sql
   ALTER TABLE EMP
   	RENAME COLUMN ename to new_ename;
   ```

   - <b>RENAME COLUMN</b> 변경하고 싶은 칼럼 <b>to</b> 새로운 칼럼명

#### ③ 테이블 삭제

- <b>DROP TABLE</b>문을 사용해서 삭제 가능

- 테이블의 구조와 데이터를 모두 삭제

- ##### DROP TABLE 테이블명 CASECADE CONSTRANT

  - 해당 테이블의 데이터를 외래키로 참조한 슬레이브 테이블과 관련된 제약사항 삭제할 때 사용

#### ④ 뷰 생성과 삭제

- 테이블로부터 유도된 가상의 테이블이 <b>뷰</b>
- <b>실제 데이터를 가지고 있지 않고</b> 테이블을 참조해서 원하는 칼럼만을 조회할 수 있게 함
- 뷰는 데이터 딕셔너리에 SQL문 형태로 저장하되 실행 시에 참조

- ##### 뷰의 특징

  - 참조한 테이블이 변경되면 뷰도 변경
  - 뷰의 검색은 참조한 테이블과 동일하게 할 수 있지만 뷰에 대한 입력, 수정, 삭제에는 제약이 있음
  - 특정 칼럼만 조회시켜서 보안성을 향상시킴
  - 한번 생성된 뷰는 변경할 수 없고 변경을 원하면 삭제 후 재생성해야 함
  - <b>ALTER</b>문을 사용해서 뷰를 변경할 수 없음

- 뷰를 생설할 때 <b>CREATE VIEW</b>문을 사용하며 이때 참조한 테이블은 <b>SELECT</b>문으로 지정

  ```sql
  // 뷰 생성
  CREATE VIEW T_EMP(뷰 테이블 이름) AS
  	SELECT * FROM EMP;
  // 뷰 조회
  SELECT * FROM T_EMP;
  ```

- 뷰를 삭제할 때는 <b>DROP VIEW</b>사용

- 뷰를 삭제했다고 해서 참조했던 테이블이 삭제되지 않음

  ```sql
  DROP VIEW T_EMP;
  ```

##### ▶뷰의 장점과 단점

- ##### 장점

  - 특정 칼럼만 조회할 수 있기 때문에 <b>보안 기능</b>이 있음
  - 데이터 관리가 간단함
  - SELECT 문이 간단해짐
  - 하나의 테이블에 여러 개의 뷰를 생성할 수 있음

- ##### 단점

  - 뷰는 독자적인 인덱스를 만들 수 없음
  - 삽입, 수정, 삭제 연산이 제약
  - 데이터 구조를 변경할 수는 없음



### 4. DML (Data Manipulation Language)

#### ① INSERT

1. ##### INSERT문

   - 테이블에 데이터를 입력하는 <b>DML</b>문임

     ```sql
     INSERT INTO 테이블명 (컬럼명1, 컬럼명2) VALUES (값1, 값2);
     ```

   - 데이터를 입력할 때 문자열을 입력하는 경우에는 작은따옴표(' ')를 사용

   - 모든 칼럼에 대한 데이터를 삽입하는 경우에는 칼럼명을 생략할 수 있다

     - 대신 모든 칼럼에 데이터를 입력

     ```sql
     INSERT INTO 테이블명 VALUES (모든 칼럼 값);
     ```

   - <b>Auto Commint</b>을 설정하지 않으면 <b>INSERT</b>문을 실행했다고 데이터 파일에 저장되는 것은 아님. 최종적으로 <b>TCL</b>문인 <b>Commit</b>을 실행해야함

2. ##### SELECT문으로 입력

   - <b>SELECT</b>문을 사용하여 데이터를 조회해서 해당 테이블에 바로 삽입할 수 있음

   - 단, 입력되는 테이블은 사전에 생성되어 있어야 함

     ```sql
     INSERT INTO DEPT_TEST
     	SELECT * FROM DEPT;
     ```

3. ##### Nologging 사용

   - 데이터베이스에 데이터를 입력하면 로그파일에 그 정보를 기록함

   - <b>Check point</b>라는 이벤트가 발생하면 로그파일의 데이터를 데이터 파일에 저장

   - Nologging 옵션은 로그파일의 기록을 최소화시켜서 입력 시 성능을 향상시키는 방법임

   - Nologging 옵션은 Buffer Cache라는 메모리 영역을 생략하고 기록

     ```sql
     ALTER TABLE DEPT NOLOGGING;
     ```


#### ② UPDATE

- 입력된 데이터의 값을 수정
- UPDATE문을 사용하여 원하는 조건으로 데이터를 검색해서 해당 데이터를 수정할 수 있음
- 만약, UPDATE문에 조건문을 입력하지 않으면 모든 데이터가 수정되므로 유의해야함

- UPDATE문에서 주의사항은 데이터를 수정할 때 조건절에서 검색되는 행 수만큼 수정됨

#### ③ DELETE

- 원하는 조건을 검색해서 해당되는 행을 삭제
- 조건문을 입력하지 않으면 모든 데이터가 삭제됨
- 즉, 테이블에 있는 데이터가 모두 삭제
- <b>DELETE</b>문으로 데이터를 삭제한다고 해서 테이블의 용량이 초기화되지 않음

##### ▶테이블의 모든 데이터삭제

- ##### DELETE FROM 테이블명;

  - 테이블의 모든 데이터를 삭제
  - 데이터가 삭제되어도 테이블의 용량은 감소하지 않음

- ##### TRUNCATE TABLE 테이블명;

  - 테이블의 모든 데이터를 삭제함
  - 데이터가 삭제되면 <b>테이블의 용량은 초기화</b>됨
  - 테이블의 구조는 삭제되지 않음

#### ④ SELECT

1. ##### SELECT문 사용

   - 데이터에 입력된 데이터를 조회하기 위해서 <b>SELECT</b>문을 사용
   - 특정 칼럼이나 특정 행만을 조회할 수 있음

##### ▶SELECT 칼럼 지정

- ##### SELECT ENAME || '님' FROM EMP;

  - EMP 테이블의 모든 행에서 ENAME 칼럼을 조회
  - 단, ENAME 칼럼 뒤에 '님' 이라는 문자를 결합
  - 예) <b>임베스트 님</b>이라고 출력

2. ##### ORDER BY를 사용한 정렬

   - <b>ORDER BY</b>는 데이터를 오름차순(Ascending) 혹은 내림차순(Descending)으로 출력

   - 정렬을 하는 시점은 모든 실행이 끝난 후에 데이터를 출력해 주기 바로 전임
   - <b>ORDER BY</b>는 정렬을 하기 때문에 데이터베이스 메모리를 많이 사용하게 됨
     즉, 대량의 데이터를 정렬하게 되면 정렬로 인한 성능 저하가 발생
   - 정렬을 회피하기 위해서 인덱스를 생성할 때 사용자가 원하는 형태로 오름차순 혹은 내림차순으로 생성해야 함
   - 특별한 지정이 없으면 <b>ORDER BY</b>는 오름차순으로 정렬

3. ##### Index를 사용한 정렬 회피

   - 정렬은 부하를 주므로, 인덱스를 사용해서 <b>Order By</b>를 회피할 수 있음

   - ##### SELECT /*+ INDEX_DESC(A) */ FROM EMP A;

     - 내림차순으로 읽게 지정
     - 따라서 SELECT문에 <b>ORDER BY EMPNO DESC</b>를 사용하지 않음

4. ##### DISTINCT와 Alias

   - ##### DISTINCT

     - 칼럼명 앞에 지정하여 중복된 데이터를 한 번만 조회하게 함

     - ##### SELECT DISTINCT 컬럼명

   - ##### Alias

     - 테이블명이나 칼럼명이 너무 길어서 간락하게 할 때 사용

     - ##### SELECT 컬럼명 AS "이름"



### 5. WHERE문 사용

1. ##### WHERE문이 사용하는 연산자

   ##### ▶비교 연산자

   - <b>=</b> : 같은 것을 조회
   - <b><</b> : 작은 것을 조회
   - <b><=</b> : 작거나 같은 것을 조회
   - <b>< </b>:큰 것을 조회
   - <b>>=</b> :크거나 같은 것을 조회

   ##### ▶부정 비교 연산자

   - <b>!= </b>: 같지 않은 것을 조회
   - <b>^=</b> : 같지 않은 것을 조회
   - <b><></b> : 같지 않은 것을 조회
   - <b>NOT 칼럼명 = </b> : 같지 않은 것을 조회
   - <b>NOT 칼럼명 ></b> : 크지 않은 것을 조회

   ##### ▶논리 연산자

   - <b>AND</b> : 조건을 모두 만족해야 참이 됨
   - <b>OR</b> : 조건 중 하남나 만족해도 참이 됨
   - <b>NOT</b> : 참이면 거짓으로 바꾸고 거짓이면 참으로 바꿈

   ##### ▶SQL 연산자

   - <b>LIKE '%비교 문자열%'</b> : 비교 문자열을 조회함, '%'는 모든 값을 의미
   - <b>BETWEEN A AND B</b> : A와 B 사이의 값을 조회
   - <b>IN (list)</b> : OR를 의미하며 list 값 중에 하나만 일치해도 조회
   - <b>IS NULL</b> : NULL 값을 조회

   ##### ▶부정 SQL 연산자

   - <b>NOT BETWEEN A AND B</b> : A와B 사이의 해당되지 않는 값을 조회
   - <b>NOT IN (list)</b> : list와 불일치한 것을 조회
   - <b>IS NOT NULL</b> : NULL 값이 아닌 것을 조회

2. ##### LIKE문

   - <b>LIKE문</b>은 와일드카드를 사용해서 데이터를 조회할 수 있음

   ##### ▶와일드카드

   - ##### %

     - 어떤 문자를 포함한 모든 것을 조회
     - 예를 들어 '조%'는 '조'로 시작하는 모든 문자를 조회

   - ##### _

     - 한 개인 단일 문자를 의미

   ```sql
   SELECT * FROM emp
   WHERE ename LIKE 'test%';
   ```

   - <b>test</b>로 시작하는 모든 데이터를 조회하게 됨

   ```sql
   SELECT * FROM emp
   WHERE ename LIKE '%1';
   ```

   - 마지막이 <b>1</b>로 끝나는 모든 데이터를 조회하게 됨

   ```sql
   SELECT * FROM emp
   WHERE ename LIKE '%est%';
   ```

   - 중간에 <b>est</b>가 있는 모든 데이터를 조회하게 됨

   ```sql
   SELECT * FROM emp
   WHERE ename LIKE 'test1';
   ```

   - <b>LIKE</b>문에 <b>와일드카드</b>를 사용하지 않으면 <b>=</b>와 같음
   - 즉, 일치하는 값만 조회

   ```sql
   SELECT * FROM emp
   WHERE ename LIKE 'test_';
   ```

   - 칼럼에서 <b>test</b>로 시작하고 하나의 글자만 더 있는 것을 조회 함
   - 즉, <b>'_'</b> 하나 당 글자 수 하나

3. ##### BETWEEN문

   - 지정된 범위에 있는 값을 조회

   ```sql
   SELECT * FROM emp
   WHERE SAL BETWEEN 1000 AND 2000;
   ```

   - <b>SAL</b>값이 1000 이상 2000 이하 사이의 값을 조회

   ```sql
   SELECT * FROM emp
   WHERE SAL NOT BETWEEN 1000 AND 2000;
   ```

   - <b>SAL</b>값이 1000 미만 2000 초과인 값을 조회

4. ##### IN문

   - <b>OR</b>의 의미를 가지고 있어서 하나의 조건만 만족해도 조회가 됨

   - 직업이 <b>CLERK</b>이거나 <b>MANAGER</b>인 것을 조회할 때는 ?

     - ##### JOB IN ('CLERK', 'MANAGER')

   - 여러 개의 칼럼을 지정할 때

     - ##### WHERE (JOB, ENAME) IN ( ('CLERK', 'TEST1'), ('MANAGER', 'test4') )

     - 직업이 <b>CLERK</b>이고 이름이 <b>test1</b>이거나 <b>MANAGER</b>이고 <b>test4</b>인 경우에 조회 함
       조건이 두 개 이상인 경우에는 조건을 만족하는 것은 <b>AND</b>여야 하고 그 중에서 만족하는 값을 가져오는 건 <b>OR</b>임

5. ##### NULL 값 조회

   1. ##### NULL의 특징

      - 모르는 값을 의미
      - 값의 부재를 의미
      - NULL과 숫자 혹은 날짜를 더하면 NULL이 됨
      - NULL과 어떤 값을 비교할 때, <b>'알 수없음'</b>이 반환됨

   2. ##### NULL값 조회

      - NULL을 조회할 경우는 <b>IS NULL</b>을 사용함
      - NULL 값이 아닌 것을 조회할 경우는 <b>IS NOT NULL</b>을 사용

   3. ##### NULL 관련 함수

      - ##### NVL 함수 (Oracle)

        - NULL이면 다른 값으로 바꾸는 함수
        - <b>NVL(num, 0)</b>은 <b>num</b>칼럼이 <b>NULL</b>이면 <b>0</b>으로 바꿈

      - ##### NVL2 함수 (Oracle)

        - <b>NVL 함수</b>와 <b>DECODE</b> 함수를 하나로 만든 것
        - <b>NVL2(num, 1, 0)</b>은 <b>num</b>칼럼이 <b>NULL</b>이 아니면 <b>1</b>을 <b>NULL</b>이면 <b>0</b>을 반환

      - ##### NULLIF 함수 (Oracle, MS-SQL, MySQL)

        - 두 개의 값이 같으면 <b>NULL</b>을 같지 않으면 첫 번째 값을 반환
        - <b>NULLIF(ex1, ex2)</b>은 <b>ex1</b>과 <b>ex2</b>가 같으면 <b>NULL</b>을 반환하고 같지 않으면 <b>ex1</b>을 반환함

      - ##### COALESCE (Oracle, MS-SQL)

        - <b>NULL</b>이 아닌 최초의 인자 값을 반환
        - <b>COALESCE(ex1, ex2, ex3, ...)</b>은 <b>ex1</b>이 <b>NULL</b>이 아니면 <b>ex1</b>의 값을, 그렇지 않으면 그 뒤의 값의 <b>NULL</b> 여부를 판단하여 값을 반환
        - 즉, <b>NULL</b>값이 아닌 최초의 값을 찾아서 반환하는 것



### 6. GROUP 연산

#### ① GROUP BY문

- 테이블에서 소규모 행을 그룹화하여 <b>합계, 평균, 최댓값, 최솟값</b> 등을 계산함

- <b>HAVING</b>구에 조건문을 사용

- <b>Grouping</b>된 결과에 대한 조건문을 사용

- <b>ORDER BY</b>를 사용해서 정렬을 할 수 있음

  ```sql
  SELECT DEPTNO, SUM(SAL)
  FROM EMP
  GROUP BY DEPTNO
  ```

  - <b>DEPTNO</b>를 기준으로 그룹으로 묶고 그룹별 합계를 계산하라는 것

#### ② HAVING문

- GROUP BY에 조건절을 사용하려면 HAVING을 사용해야 함
- 만약 WHERE절에 조건문을 사용하게 되면 조건을 충족하지 못하는 데이터들은 GROUP BY 대상에서 제외됨

#### ③ 집계 함수 종류

- ##### COUNT()

  - 행의 수를 조회

- ##### SUM()

  - 합계를 계산

- ##### AVG()

  - 평균을 계산

- ##### MAX()와 MIN()

  - 최댓값과 최솟값을 계산

- ##### STDDEV()

  - 표준편차를 계산

- ##### VARIANCE()

  - 분산을 계산

#### ④ COUNT 함수

- <b>COUNT(*)</b>는 NULL값을 포함한 모든 행수를 계산
- <b>COUNT(칼럼명)</b>는 NULL값을 제외한 행 수를 계산



### 7. SELECT문 실행 순서

- FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY



### 8. 명시적 형변환과 암시적 형변환

- 형변환이라는 것은 두 개의 데이터의 데이터 타입(형)이 일치하도록 변환하는 것

- ##### 명시적 형변환

  - 형변환 함수를 사용해서 데이터 타입을 일치시키는 것으로 SQL을 사용할 때 형변환 함수를 사용

  - ##### 형변환 함수

    - ##### TO_NUMBER(문자열)

      - 문자열을 숫자로 변환함

    - ##### TO_CHAR(숫자 혹은 날짜, [FORMAT])

      - 숫자 혹은 날짜를 지정된 FORMAT의 문자로 변환함

    - ##### TO_DATE(문자열, FORMAT)

      - 문자열을 지정된 FORMAT의 날짜형으로 변환

- ##### 암시적 형변환

  - 개발자가 형변환을 하지 않은 경우 데이터베이스 관리 시스템이 자동으로 형변환하는 것

- 인덱스 칼럼에 형변환을 수행하면 인덱스를 사용하지 못함

  - 쿼리내에 <b>암시적 형변환</b>이 사용될 때 인덱스를 사용할 수 없음
  - 즉, <b>명시적 형변환</b>을 이용하여 쿼리가 실행되기 전에 형변환을 해주면 사용할 수 있음



### 9. 내장형 함수

#### ① 내장형 함수의 종류

##### ▶문자열 함수

- ##### ASCII(문자)

  - 문자 혹은 숫자를 ASCII 코드값으로 변환

- ##### CHR/CHAR(ASCII 코드값)

  - ASCII 코드값을 문자로 변환
  - 오라클은 <b>CHR</b> 사용, MSSQL, MYSQL은 <b>CHAR</b>사용

- ##### SUBSTR(문자열, n, m)

  - 문자열에서 n번째 위치부터 m개를 자름

- ##### CONCAT(문자열1, 문자열2)

  - 문자열1과 문자열2를 결합함
  - 오라클은 <b>||</b>, MSSQL은 <b>+</b>를 사용할 수 있음

- ##### LOWER(문자열)

  - 영문자를 소문자로 변환

- ##### UPPER(문자열)

  - 영문자를 대문자로 변환

- ##### LENGTH 혹은 LEN(문자열)

  - 공백을 포함해서 문자열의 길이를 알려줌

- ##### LTRIM(문자열, 지정문자)

  - 왼쪽에서 지정된 문자를 삭제
  - 지정된 문자를 생략하면 공백을 삭제

- ##### RTRIM(문자열, 지정문자)

  - 오른쪽에서 지정된 문자를 삭제
  - 지정된 문자를 생략하면 공백을 삭제

- ##### TRIM(문자열, 지정문자)

  - 왼쪽 및 오른쪽에서 지정된 문자를 삭제
  - 지정된 문자를 생략하면 공백을 삭제

##### ▶날짜형 함수

- ##### SYSDATE

  - 오늘 날짜를 구하는 함수

- ##### EXTRACT

  - 해당 연, 월, 일을 구하는 함수
  - <b>EX )</b> EXTRACT(YEAR FROM sysdate)
    - 년도만 나옴

##### ▶숫자형 함수

- ##### ABS(숫자)

  - 절대값을 돌려줌

- ##### SIGN(숫자)

  - 양수, 음수, 0을 구별
  - 순서대로 1, -1, 0을 반환

- ##### MOD(숫자1, 숫자2)

  - 숫자1을 숫자2로 나누어 나머지를 계산
  - %를 사용해도 됨

- ##### CEIL/CEILING(숫자)

  - 숫자보다 크거나 같은 최소의 정수를 돌려줌

- ##### FLOOR(숫자)

  - 숫자보다 작거나 같은 최대의 정수를 돌려줌

- ##### ROUND(숫자, m)

  - 소수점 m자리에서 반올림
  - m의 기본값은 0

- ##### TRUNC(숫자, m)

  - 소수점 m 자리에서 절삭
  - m의 기본값은 0



### 10. DECODE와 CASE문

#### ① DECODE

- DECODE문으로 IF문을 구현할 수 있ㅇㅁ

- 즉, 특정 조건이 참이면 A, 거짓이면 B로 응답

  ```sql
  DECODE(EMPNO, 1000, 'TRUE', 'FALSE')
  ```

  - ENPNO가 1000이면 TRUE를 출력하고 다르면 FALSE를 출력

#### ② CASE문

- IF ~ THEN ~ ELSE-END의 프로그래밍 언어처럼 조건문을 사용할 수 있음

- 조건을 WHERE구에 사용

- 해당 조건이 참이면 THEN이 실행, 거짓이면 ELSE구가 실행

  ```sql
  SELECT CASE
  		WHEN EMPNO = 1000 THEN 'A'
  		WHEN EMPNO = 2000 THEN 'B'
  		ELSE C
  	END
  FROM EMP
  ```



### 11. ROWNUM과 ROWID

#### ① ROWNUM

- ORACLE 데이터베이스의 SELECT문 결과에 대해서 논리적인 일련번호를 부여함

- 조회되는 행 수를 제한할 때 많이 사용

- 화면에 데이터를 출력할 때 부여되는 논리적 순번

- 만약 ROWNUM을 사용해서 페이지 단위 출력을 하기 위해서는 인라인 뷰를 사용해야함

  - ##### 인라인 뷰

    - SELECT문에서 FROM절에 사용되는 서브쿼리를 의미

  ```sql
  SELECT *
  FROM (SELECT ROWNUM as list, ENAME
  	  FROM EMP)
  WHERE list <= 5;
  ```

  - 5건을 조회

- SQL Server에서는 TOP구문을 사용

- MySQL에서는 limit구문을 사용

#### ② ROWID

- 테이블에 데이터를 입력하면 자동으로 생성되는 값

- ORACLE 데이터베이스 내에서 데이터를 구분할 수 있는 유일한 값

- SELECT문으로 확인할 수 있음

- ROWID를 통해서 데이터가 어떤 데이터 파일, 어느 블록에 저장되어 있는 지 알 수 있음

- ##### 오브젝트 번호 (1 ~ 6)

  - 오브젝트 별로 유일한 값을 가지고 있으며, 해당 오브젝트가 속해 있는 값

- ##### 상대 파일 번호 (7 ~ 9)

  - 테이블스페이스에 속해 있는 데이터 파일에 대한 상대 파일번호

- ##### 블록 번호 (10 ~ 15)

  - 데이터 파일 내부에서 어느 블록에 데이터가 있는지 알려줌

- ##### 데이터 번호 (16 ~ 18)

  - 데이터 블록에 데이터가 저장되어 있는 순서를 의미



### 12. WITH구문

- 서브쿼리를 사용해서 임시 테이블이나 뷰처럼 사용할 수 있는 구문

- 서브쿼리 블록에 별칭을 지정할 수 있음

- 옵티마이저는 SQL을 인라인 뷰나 임시 테이블로 판단

  ```sql
  WITH viewData AS
  	(SELECT * FROM EMP WHERE DEPTNO = 30)
  SELECT * FROM viewData;
  ```



### 13. DCL(Data Control Language)

#### ① GRANT

- 데이터베이스 사용자에게 권한을 부여

- 데이터베이스 사용을 위해서는 권한이 필요하며 <b>연결, 입력, 수정, 삭제, 조회</b>를 할 수 있음

  ```sql
  GRANT privileges ON object TO user;
  ```

  - <b>privileges</b>는 권한을 의미하며 <b>object</b>는 테이블명임
  - <b>user</b>는 Oracle 데이터베이스 사용자를 지정하면 됨

- 권한 종류

  - SELECT, INSERT, UPDATE, DELETE, REFERENCES(제약조건), ALTER, INDEX, ALL

- ##### WITH GRANT OPTION

  - 특정 사용자에게 권한을 부여할 수 있는 권할을 부여
  - 권한을 A 사용자가 B에 부여하고 B가 다시 C를 부여한 후에 권한을 취소하면 모든 권한이 회수됨

- ##### WITH ADMIN OPTION

  - 테이블에 대한 모든 권한ㅇ늘 부여
  - 권한을 A 사용자가 B에 부여하고 B가 다시 C에게 부여한 후에 권한을 취소하면 B 사용자 권한만 취소

  ```sql
  GRANT SELECT, INSERT, UPDATE, DELETE
  ON EMP
  TO LIMBEST WITH GRANT OPTION
  ```

#### ② REVOKE

- 데이터베이스 사용자에게 부여된 권한을 회수

  ```sql
  REVOKE privileges ON object FROM user;
  ```



### 14. TCL(Transaction Control Language)

#### ① COMMIT

- INSERT, UPDATE, DELETE문으로 변경한 데이터를 데이터베이스에 반영함
- COMMIT이 완료되면 데이터베이스 변경으로 인한 LOCK이 해제됨
- COMMIT이 완료되면 다른 모든 데이터베이스 사용자는 변경된 데이터를 조작할 수 있음
- COMMIT을 실행하면 하나의 트랜잭션 과정을 종료

#### ② ROLLBACK

- ROLLBACK을 실행하면 데이터에 대한 변경 사용을 모두 취소하고 트랜잭션을 종료
- 이전에 COMMIT한 곳까지만 복구

#### ③ SAVEPOINT(복구점)

- 트랜잭션을 작게 분할하여 관리하는 것으로 SAVEPOINT를 사용하면 지정된 위치 이후의 트랜잭션만 ROLLBACK할 수 있음

- ##### SAVEPOINT <SAVEPOINT명>

- 지정된 SAVEPOINT까지만 데이터 변경을 취소하고 싶은 경우는 <b>ROLLBACK TO <SAVEPOINT명></b>을 실행

- <b>ROLLBACK</b>을 실행하면 <b>SAVEPOINT</b>와 관계없이 데이터의 모든 변경사항을 저장하지 않음







