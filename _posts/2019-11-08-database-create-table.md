---
layout: post
title: "[MySQL] 테이블 추가 : create table"
categories:
  - Database
tags:
  - database
  - mysql
  - create

last_modified_at: 2019-11-08T
---
# create table

### 기본 형식
```sql
create table '테이블명' (
  '칼럼명' '데이터타입' (not null),
  '칼럼명' '데이터타입' (not null),
  '칼럼명' '데이터타입' (default '값'),
  ...,
  primary key ('칼럼명'),
  (unique ('칼럼명')),
  (foreign key ('칼럼명') references '테이블명'('칼럼명'))
  (on delete cascade(or 'set null' or 'set default')
  (on update cascade)
) ENGINE=InnoDB;
```

---

#### 예제1
```sql
create table STUDENT (
  Name varchar(10) not null,
  Student_number integer not null,
  class integer default 1,
  Major varchar(10) not null,
  primary key (Student_number),
  unique (Name)
) ENGINE=InnoDB;
```

---

#### 예제2
```sql
create table GRADE_REPORT (
  Student_number integer not null,
  Section_identifier integer not null,
  Grade varchar(4),
  primary key (Student_number, Section_identifier),
  foreign key (Student_number) references STUDENT(Student_number)
  on delete cascade
  on update cascade,
  foreign key (Section_identifier) references SECTION(Section_identifier)
  on delete cascade
  on update cascade
) ENGINE=InnoDB;
```

---
