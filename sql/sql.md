# SQL



## 목차



### DB

- 데이터베이스는 체계화된 데이터의 모임이다
- 여러사람이 공유하고 사용할 목적으로 통합 관리되는 정보의 집합이다.
- 논리적으로 연관된 자료의 모음
- 그 내용을 고도로 구조화 검색과 생산의 효율화를 꾀한 것
- 몇 개의 자료 파일을 조직적으로 통합하여, 자료 항목의 중복을 없애고 자료를 구조화하여 기억시켜 놓은 자료의 집합체

### DB로 얻는 장점들

- 데이터 중복 최소화
- 데이터 무결성(정확한 정보를 보장)
- 데이터 일관성
- 데이터 독립성 (물리적 / 논리적)
- 데이터 표준화
- 데이터 보안 유지

### RDB(관계형 데이터 베이스)

- Schema > 데이터 베이스에서 자료의 구조, 표현방법, 관계등 전반적인 명세를 기술한 것
- Table : 열과 행으로 모델을 사용해 조직된 데이터 요소들의 집합
- Column(열) > 세로, 필드
- row(행) > 가로, 레코드
- PK(기본키) : 각 행의 고유 값

### SQL

#### DDL - 데이터 정의 언어(Data Definition Language)

- 관계형 데이터 베이스 구조(테이블, 스키마)를 정의하기 위한 명령어
  - CREATE : 데이터베이스에서 테이블 생성

  ```sql
  CREATE TABLE classamtes(
  id INTEGER PRIMARY KEY,
  name TEXT
  );
  
  CREATE TABLE classamtes(
  name TEXT
  age INT,
  address TEXT
  );
  
  CREATE TABLE classamtes(
  id INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  age INT NOT NULL,
  address TEXT NOT NULL
  );
  
  #SQLite는 기본적으로 id를 재사용한다
  #이를 막기 위해서는
  CREATE TABLE classamtes(
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  age INT NOT NULL,
  address TEXT NOT NULL
  );
  ```

  - DROP : 데이터베이스에서 테이블 제거

  ```sqlite
  DROP TABLE classmates;
  ```

  - ALTER

#### DML - 데이터 조작 언어(Data Manipulation Language)

- 데이터를 저장, 조회, 수정, 삭제 등을 하기 위한 명령여
  - INSERT : 새로운 데이터 삽입(추가)

  ```sql
  INSERT INTO classmates (name, age) VALUES ('홍길동', 23);
  
  INSERT INTO classmates VALUES ('홍길동', 30, '서울')
  # 모든 열에 데이터가 있는 경우 column을 명시하지 않아도 됨!
  
  SELECT rowid, * FROM classmates;
  #SQLite는 따로 PRIMARY KEY 속성의 컬럼을 작성하지 않으면, 값이 자동으로 증가하는 Pk 옵션을 가진 rowid 컬럼을 정의
  
  INSERT INTO classmates VALUES
  ('홍길동', 30, '서울'),
  ('김철수', 30, '대전'),
  ('최전가', 28, '부산');
  ```

  - SELECT : 저장되어있는 데이터 조회
    - 테이블에서 데이터를 조회
    - SELECT 문은 SQLite 에서 가장 복잡한 문이며 다양한 절(clause)와 함께 사용
    - ORDER BY, DISTINCT, WHERE, LIMIT, GROUP BY...
    - LIMIT : 쿼리에서 반환되는 행 수를 제한
    - WHERE : 쿼리에서 반환된 행에 대한 특정 검색 조건을 지정

  ```sql
  CREATE TABLE users(
  first_name TEXT NOT NULL,
  last_name TEXT NOT NULL,
  age INTEGER NOT NULL,
  country TEXT NOT NULL,
  phone TEXT NOT NULL,
  balance INTERGER NOT NULL,
  );
  
  sqlite> .mode csv
  sqlite> .import users.csv users
  sqlite> .tables
  
  #users 테이블에서 age가 30 이상인 유저의 모든 컬럼 정보를 조회하려면?
  SELECT * FROM users WHERE age >= 30;
  #users 테이블에서 age가 30 이상인 유저의 이름만 조회하려면?
  SELECT first_name FROM users WHERE age>=30;
  #users 테이블에서 age가 30 이상이고 성이 '김'인 사람의 나이와 성만 조회하려면?
  SLECET age, last_name FROM users WHERE age>=30 AND last_name='김'
  ```

  - DISTINCT : 조회 결과에서 중복 행을 제거(DISTINCT 절은 SELECT 키워드 바로 뒤에 작성해야 함)

  ```sql
  #모든 컬럼 값이 아닌 특정 컬럼만 조회하기
  #classamtes 테이블에서 id, name 컬럼 값만 조회
  SELECT rowid, name FROM classmates;
   
  #원하는 수 만큼 데이터 조회하기
  #classamtes 테이블에서 id,anme 컬럼 값을 하나만 조회
  SELECT rowid, name FROM classmates LIMIT 1;
    
  #특정 부분에서 원하는 수 만큼 데이터 조회하기
  #classmates 테이블에서 id, name 컬럼 값을 세번째에 있는 하나만 조회
  SELECT rowid, name FROM classmates LIMIT 1 OFFSET 2;
  
  #특정 데이터(조건) 조회하기
  #classmates 테이블에서 id,name 컬럼 갓 중에 주소가 서울인 경우의 데이터를 조회
  SELECT rowid, name FROM classmates WHERE address='서울';
  
  #특정 컬럼을 기준으로 중복없이 가져오기
  #classamtes 테이블에서 age값 전체를 중복없이 조회하세요
  SELECT DISTINCT age FROM classamtes;
   
  ```

  - UPDATE : 저장되어있는 데이터 갱신

  ```sql
  #rowid 기준으로 수정하기!
  #classmates 테이블에 id가 5인 레코드를 수정
  #이름을 홍길동으로, 주소를 제주도로 바꿔보자
  UPDATE classmates SET name='홍길동', address='제주도' WHERE rowid=5;
  ```

  

  - DELETE : 저장되어있는 데이터 삭제

  ```sql
  #rowid 기준으로 삭제하기
  #classmates 테이블에 id가 5인 레코드 삭제
  DELETE FROM classmates WHERE rowid=5;
  ```



#### DCL - 데이터 제어 언어(Data Control Language)

- 데이터베이스 사용자의 권한 제어를 위해 사용하는 명령어
  - GRANT
  - REVOKE
  - COMMIT
  - ROLLBACK

### Sqlite Functions

- Count : 그룹의 항목 수를 가져옴

```sql
#users 테이블의 레코드 총 개수를 조회한다면?
SELECT COUNT(*) FROM users;
```

- AVG : 값 집합의 평균 값을 계산
- MAX : 그룹에 있는 모든 값의 최대값을 가져옴
- MIN : 그룹에 있는 모든 값의 최소값을 가져옴
- SUM : 모든 값의 합을 계산

```sql
#30살 이상인 사람들의 평균 나이는?
SELECT AVG(age) FROM users WHERE age>=30;
#계좌 잔액(balance)이 가장 높은 사람과 그 액수를 조회하려면?
SELECT first_name, MAX(balance) FROM users;
#나이가 30 이상인 사람의 계좌 평균 잔액을 조회하려면?
SELECT AVG(balacne) FROM users WHERE age>=30;
```

- LIKE
  - 패턴 일치를 기반으로 데이터를 조회하는 방법
  - sqlite는 패턴 구성을 위한 2개의 wildcards를 제공
    - % : 0개 이상의 문자
    - _ : 임의의 단일 문자

```sql
SELECT * FROM 테이블 WHERE 컬럼 LIKE '와일드카드패턴'
```

| 와일드카드패턴 |                     의미                      |
| :------------: | :-------------------------------------------: |
|       2%       |                2로 시작하는 값                |
|       %2       |                 2로 끝나는 값                 |
|      %2%       |                2가 들어가는 값                |
|      _2%       | 아무 값이 하나 있고 두번 째가 2로 시작하는 값 |
|    1_ _ _ _    |          1로 시작하고 총 4자리인 값           |
| 2_%_%, 2 _ _ % |        2로 시작하고 적어도  3자리인 값        |

```sqlite
#useres 테이블에서 나이가 20대인 사람만 조회해보자
SELECT * FROM useres WHERE age LIKE '2_';

#useres 테이블에서 지역 번호가 02인 사람만 조회해보자
SELECT * FROM users WHERE phone LIKE '02_%';

#users 테이블에서 이름이 '준'으로 끝나는 사람만 조회해보자
SELECT * FROM users WHERE first_name LIKE '%준';

#users 테이블에서 중간 번호가 5114인 사람만 조회한다면?
SELECT * FROM users WHERE phone LIKE '%-5114-%';
```

- ORDER BY
  - 조회 결과 집합을 정렬
  - SELECT 문에 추가하여 사용
  - 정렬 순서를 위한 2개의 keyword 제공
    - ASC - 오름차순(default)
    - DESC - 내림차순

```sqlite
#users 에서 나이 순으로 오름차순 정렬하여 상위 10개만 조회해보자
SELECT * FROM users ORDER BY age ASC LIMIT 10;

#나이 순, 성 순으로 오름차순 정렬하여 상위 10개만 조회해보자
SELECT * FROM users ORDER BY age, last_name ASC LIMIT 10;

#게좌 잔액 순으로 내림차순 정렬하여 해당 유저의 성과 이름을 10개만 조회한다면?
SELECT last_name, first_name FROM users ORDER BY balance DSEC LIMIT 10;
```

- GROUP BY
  - 행 집합에서 요약 행 집합을 만듦
  - SELECT 문의 optional 절
  - 선택된 행 그룹을 하나 이상의 열 값으로 요약 행으로 만듦
  - 문장에 WHERE 절이 포함된 경우 반드시 WHERE 절 뒤에 작성해야 함

```sqlite
#useres에서 각 성(last_name)씨가 몇 명씩 있는지 조회한다면?
SELECT last_name, COUNT(*) FROM users GROUP BY last_name;

#as를 활용해서 COUNT에 해당하는 컬럼 명을 바꿔서 조회할 수 있음
SELECT last_name, COUNT(*) AS name_count FROM users GROUP BY last_name;
```

- ALTER TABLE
  - table 이름 변경
  - 테이블에 새로운 column 추가
  - column 이름 수정(sqlite 3.25.0 부터 지원)

```sqlite
#테이블 이름 변경
ALTER TABLE articles RENAME TO news;

# 테이블 컬럼 추가
ALTER TABLE news ADD COLUMN crated_at TEXT NOT NULL;
# > 실패함(기존 레코드들에는 새로 추가된 필드에 대한 정보가 없다)
# (그렇기 떄문에 not null형태의 컬럼은 추가가 불가능)
#이를 해결해기 위에서는 1. NOT NULL 설정 없이 추가하기 2. 기본 값(DEFAULT) 설정하기

ALTER TABLE news ADD COLUMN subtitle TEXT NOT NULL DEFAULT '소제목';
```

