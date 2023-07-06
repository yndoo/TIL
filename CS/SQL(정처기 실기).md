## NULL 값은 "NONE"으로 출력하기?
### COALESCE
* `COALESCE(col1, col2)` 는 인자로 주어진 컬럼들 중에서 NULL 값이 아닌 첫 번째 값을 반환하는 함수
* `COALESCE(col1, 0)` 는 col1 컬럼의 모든 NULL 값을 0으로 변환하여 출력

* https://school.programmers.co.kr/learn/courses/30/lessons/132201  
```sql
SELECT PT_NAME, PT_NO, GEND_CD, AGE, COALESCE(TLNO, "NONE") FROM PATIENT
WHERE AGE<=12 AND GEND_CD = "W"
ORDER BY AGE DESC, PT_NAME ASC;
```
---
## 상위 n개의 레코드만 반환
### LIMIT  
* https://school.programmers.co.kr/learn/courses/30/lessons/59405
```sql
SELECT NAME FROM ANIMAL_INS
ORDER BY DATETIME LIMIT 1;
```
---
## 권한 회수
* REVOKE 명령어 사용
* `REVOKE` 권한 `ON` 테이블 `FROM` 사용자 (리온프 로 외우자)
```sql
REVOKE INSERT ON DEFT FROM 신민아;
```
## 권한 부여
* GRANT 명령어 사용
* `GRANT` 권한 `ON` 테이블 `TO` 사용자 `[WITH 권한 옵션]` (그론투 로 외우자)
```sql
GRANT ALL ON STUDENT TO SOOJEBI_SYS WITH GRANT OPTION
```
---
