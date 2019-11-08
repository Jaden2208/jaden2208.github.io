---
layout: post
title: "[MySQL] 테이블에 행 추가 : insert into"
categories:
  - Database
tags:
  - database
  - mysql
  - insert

last_modified_at: 2019-11-08T
---
# insert into TABLE

### 기본 형식
```sql
insert into '테이블명' values
  ('값', '값', '값',...),
  ...
  ('값', '값', '값',...);
```

---

#### 예제1
```sql
insert into COURSE values
  ('Intro to Computer Science', 'CS1310', 4, 'CS'),
  ('Data Structures', 'CS3320', 4, 'CS'),
  ('Discrete Mathematics', 'MATH2410', 3, 'MATH'),
  ('Database', 'CS3380', 3, 'CS');
```

---

#### 예제2
```sql
insert into GRADE_REPORT values (17, 85, null);
```

---
