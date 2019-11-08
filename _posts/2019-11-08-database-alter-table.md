---
layout: post
title: "[MySQL] 테이블 스키마 수정 : alter table"
categories:
  - Database
tags:
  - database
  - mysql
  - insert

last_modified_at: 2019-11-08T
---
# alter table

### 기본 형식과 예제

---

#### 1. 테이블에 새로운 칼럼 추가
```sql
alter table '테이블명' add column '칼럼명' '데이터타입';
```

```sql
alter table STUDENT add column Name varchar(10) not null;
```

---

#### 2. 테이블 칼럼 타입 변경
```sql
alter table '테이블명' modify column '칼럼명' '변경할 데이터타입';
```

```sql
alter table STUDENT modify column name char(4) not null;
```

---

#### 3. 테이블 칼럼 이름(+타입) 변경
```sql
alter table '테이블명' change column '기존 칼럼명' '변경할 컬럼명' '변경할 데이터타입';
```

```sql
alter table STUDENT change column name student_name char(8) not null;
```

---

#### 4. 테이블 칼럼 삭제
```sql
alter table '테이블명' drop column '칼럼명';
```

```sql
alter table STUDENT drop column course;
```

---

#### 5. primary key 추가
```sql
alter table '테이블명' add primary key ('칼럼명','칼럼명',...);
```

```sql
alter table STUDENT add primary key ('student_identifier');
```

---

#### 6. primary key 삭제
```sql
alter table '테이블명' drop primary key;
```

```sql
alter table STUDENT drop primary key;
```

---

#### 7. primary key 수정
primary key 삭제 후 새로 추가

---

#### 8. 테이블 이름 변경
```sql
alter table '기존 테이블명' rename '새 테이블명';
```

```sql
alter table STUDENT rename STUDENT_INFORMATION;
```

---
