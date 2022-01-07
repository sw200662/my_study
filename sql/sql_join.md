# SQL Join

![99219C345BE91A7E32 (1)](sql_join.assets/99219C345BE91A7E32 (1).png)

- INNER JOIN : 교집합
- LEFT / RIGHT JOIN : 부분집합
- OUTER JOIN : 합집합



ex) 테이블을 예시로 잡자

| ID   | FORA |
| ---- | ---- |
| 1    | AAAA |
| 2    | BBBB |
| 3    | CCCC |

| ID   | FORB |
| ---- | ---- |
| 1    | 가가 |
| 2    | 나나 |
| 4    | 다다 |
| 5    | 라라 |

### INNER JOIN : 둘의 교집합

```mysql
SELECT A.ID, A.FORA, A.FORB
FROM A INNER JOIN B
ON A.ID = B.ID
```

| ID   | FORA | FORB |
| ---- | ---- | ---- |
| 1    | AAAA | 가가 |
| 2    | BBBB | 나나 |

### LEFT JOIN : 조인기준 왼쪽에 있는거 모두 SELECT 된다

```sql
SELECT A.ID, A.FORA, A.FORB
FROM A LEFT OUTER JOIN B
ON A.ID = B.ID
```

| ID   | FORA | FORB |
| ---- | ---- | ---- |
| 1    | AAAA | 가가 |
| 2    | BBBB | 나나 |
| 3    | CCCC | NULL |

### LEFT JOIN - 2 : 조인기준 왼쪽에 있는것만 SELECT(A-B)

```sql
SELECT A.ID, A.FORA, A.FORB
FROM A LEFT OUTER JOIN B
ON A.ID = B.ID
WHERE B.ID IS NULL
```

| ID   | FORA | FORB |
| ---- | ---- | ---- |
| 3    | CCCC | NULL |

### RIGHT JOIN : 조인기준 오른쪽에 있는거 모두 SELECT

```sql
SELECT A.ID, A.FORA, A.FORB
FROM A RIGHT OUTER JOIN B
ON A.ID = B.ID
```

| ID   | FORA | FORB |
| ---- | ---- | ---- |
| 1    | AAAA | 가가 |
| 2    | BBBB | 나나 |
| 4    | NULL | 라라 |
| 5    | NULL | 마마 |

### RIGHT JOIN - 2 : 조인기준 오른쪽에 있는것만 SELECT

```sql
SELECT A.ID, A.FORA, A.FORB
FROM A RIGHT OUTER JOIN B
ON A.ID = B.ID
WHERE A.ID IS NULL
```

| ID   | FORA | FORB |
| ---- | ---- | ---- |
| 4    | NULL | 라라 |
| 5    | NULL | 마마 |

### OUTER JOIN : A,B가 가지고 있는 모든것

```sql
SELECT A.ID, A.FORA, A.FORB
FROM A FULL OUTER JOIN B
ON A.ID = B.ID
```

| ID   | FORA | FORB |
| ---- | ---- | ---- |
| 1    | AAAA | 가가 |
| 2    | BBBB | 나나 |
| 3    | CCCC | NULL |
| 4    | NULL | 라라 |
| 5    | NULL | 마마 |

### OUTER JOIN - 2 : 왼쪽 + 오른쪽에 있는것만(교집합 제외)

```sql
SELECT A.ID, A.FORA, A.FORB
FROM A FULL OUTER JOIN B
ON A.ID = B.ID
WHERE A.ID IS NULL OR B.ID IS NULL
```

| ID   | FORA | FORB |
| ---- | ---- | ---- |
| 3    | CCCC | NULL |
| 4    | NULL | 라라 |
| 5    | NULL | 마마 |

