# SQL에서 DDL과 DML의 차이점을 설명하고, 각각의 대표적인 명령어들의 용도를 설명하세요.

✅ DDL의 대표 명령어
CREATE -> 데이터베이스, 테이블, 인덱스, 뷰 등을 생성
ALTER	-> 기존 테이블 또는 컬럼을 수정 (컬럼 추가, 데이터 타입 변경 등)
DROP	-> 테이블, 뷰, 인덱스 등을 삭제
TRUNCATE	-> 테이블의 모든 데이터를 삭제 (구조는 유지, 롤백 불가)

✅ DML의 대표 명령어
SELECT	-> 테이블에서 데이터를 조회
INSERT	-> 테이블에 데이터를 삽입
UPDATE	-> 기존 데이터를 수정
DELETE	-> 특정 데이터를 삭제 (구조는 유지)

📌 SQL에서 DDL과 DML의 차이점 및 대표 명령어 용도
DDL은 데이터베이스의 구조를 정의하거나 변경하는 명령어로, CREATE(테이블 생성), ALTER(테이블 수정), DROP(테이블 삭제) 등이 포함되며, 실행 즉시 자동커밋되므로 롤백이 불가능하다. 반면, DML 데이터 조작 언어)은 테이블의 데이터를 조회하고 조작하는 역할을 하며, SELECT(데이터 조회), INSERT(데이터 삽입), UPDATE(데이터 수정), DELETE(데이터 삭제) 등이 있으며, 트랜잭션을 지원하여 ROLLBACK, COMMIT을 사용할 수 있다.


# 역정규화가 필요한 상황과 적용 시 고려해야 할 사항, 그리고 역정규화를 적용할 때의 장단점을 설명해주세요.

📌 역정규화가 필요한 상황
JOIN 연산이 빈번하여 성능 저하가 발생하는 경우
대량의 데이터를 처리하는 경우 (빅데이터, DW 환경)
데이터베이스 읽기 성능이 중요한 경우
자주 사용되는 데이터를 미리 계산하여 저장해야 하는 경우
분산 데이터베이스 환경에서 JOIN이 어려운 경우

📌 장단점
장점은 JOIN을 줄여 읽기 성능을 향상시키고, 쿼리 실행 속도를 최적화할 수 있다는 것이며, 단점은 데이터 중복으로 인해 저장 공간이 증가하고, 데이터 동기화 부담이 커지는 것이다.
