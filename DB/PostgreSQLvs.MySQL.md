# PostgreSQL vs MySQL  
## Schema · Database · Table 구조 차이 정리

---

## ✅ 핵심 한 줄 요약

- **PostgreSQL**
  - Database 안에 **여러 Schema**가 있고, 그 안에 Table이 있다
  - Database > Schema > Table 구조
- **MySQL**
  - **Database = Schema**, 그 안에 Table이 있다
  - Database = Schema > Table 구조

---

## 🧱 전체 구조 비교

### PostgreSQL 구조
```text
PostgreSQL Server
 └─ Database
     └─ Schema
         └─ Tables / Views / Functions / Types
```

### MySQL 구조
```text
MySQL Server
 └─ Database (= Schema)
     └─ Tables
```

⸻

## 🗄 Database 차이

### PostgreSQL
- 최상위 논리 단위
- Database 간 JOIN / FK 불가
- 보통 **서비스 단위**로 분리

```sql
CREATE DATABASE my_service;
```

### MySQL
- Database가 곧 Schema
- 내부적으로 디렉터리 개념

⸻

## Schema 차이

### PostgreSQL -> 진짜 스키
- Database 내부에 여러 Schema 존재
- 네임스페이스 역할
- 같은 이름의 테이블 가능

    ``` sql
      auth.users
      billing.users
    ```

- Schema 단위 권한 관리 가능
- 대규모 서비스 구조에 유리

### MySQL
- Schema는 Database의 별칭
- 중첩 구조 없음
- 네임스페이스 개념 없음

⸻

## Table 차이

### PostgreSQL
- Table은 **Schema 소속**
- 풀네임: `schema_name.table_name`

### MySQL
- Table은 **Database 소속**
- 풀네임: `database_name.table_name`


