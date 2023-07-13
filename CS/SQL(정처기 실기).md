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
## 집합 연산자 (UNION과 UNION ALL 다름!!)
* `UNION` : 중복 행이 제거된 쿼리 결과 반환하는 집합 연산자, 흔히 생각하는 **합집합**
* `UNION ALL` : **중복 행이 제거되지 않은** 쿼리 결과를 반환하는 집합 연산자
* `INTERSECT` : 두 쿼리 결과에 공통적으로 존재하는 결과를 반환하는 집합 연산자, **교집합**
* `MINUS` : 첫 쿼리에 있고, 두 번째 쿼리에는 없는 결과를 반환하는 집합 연산자, **차집합**
---
## DDL(Data Define Language) 데이터 정의어
* SCHEMA, DOMAIN, TABLE, VIEW, INDEX를 정의|변경|삭제
* `CREATE` 생성, `DROP` 삭제, `ALTER` 수정, `TRUNCATE` 구조유지삭제
## DCL(Data Manipulation Langauge) 데이터 조작어
* 사용자가 응용프로그램이나 질의어를 통해 데이터를 실질적으로 처리하는데 사용
* `SELECT`, `INSERT`, `DELETE`, `UPDATE`
## DCL(Data Control Language) 데이터 제어어
* 데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어들
* `GRANT` 사용자 권한 부여, `REVOKE` 사용자 권한 취소
## TCL(Transaction Control Language 트랜잭션 제어어
* 트랜잭션 결과를 허용하거나 취소하는 목적으로 사용
* `COMMIT` 확정 트랜잭션 메모리 영구저장, `ROLLBACK` 트랜잭션 저장 무효화, `CHECKPOINT` 롤백을 위한 시점 지정
---
## CREATE VIEW 하는 법
AS를 자꾸 까먹는다!!!!🥲
`CREATE VIEW` 뷰이름 `AS` 조회쿼리;  

```sql
CREATE VIEW 사원뷰 AS
SELECT 사번, 이름 FROM 사원
WHERE 성별='M';
```
---
## 테이블에 필요한 컬럼 수정하기
`ALTER TABLE` 테이블명 `MODIFY` 컬럼명 데이터타입 [제약조건];  
기억해 `알테모` ~~!!!  

```sql
ALTER TABLE 부서 MODIFY 부서번호 INTEGER PRIMARY KEY;
```
---
## 조인 JOIN 종류와 키워드  
* `[INNER] JOIN` - 내부 조인
* `LEFT [OUTER] JOIN` - 왼쪽 외부 조인
* `RIGHT [OUTER] JOIN` - 오른쪽 외부 조인
* `FULL [OUTER] JOIN` - 완전 외부 조인, 양쪽 모든 데이터 추출
* `CROSS JOIN` - 조인조건 없이 모든 데이터 보일 때 교차 조인
* `셀프조인`은 [INNER] JOIN 사용

* CROSS JOIN 말고는 모두 + `ON 조인조건`
