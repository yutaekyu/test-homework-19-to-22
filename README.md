# test-homework-19-to-22
## 19번 :CS 학과 학생의 sid, name을 sid 오름차순으로 조회하시오.

SELECT sid, name → 조회할 컬럼 지정
FROM Students → 조회 대상 테이블
WHERE dept = 'CS' → CS 학과 학생만 선택
ORDER BY sid ASC → 학번(sid) 기준 오름차순 정렬

20번 수강신청(Enroll) 기준으로 수강 중인 학과명(중복 제거)을 조회하시오.
SELECT DISTINCT s.dept
FROM Students s
JOIN Enroll e ON s.sid = e.sid;

JOIN Enroll e ON s.sid = e.sid → 수강신청 정보와 학생 정보를 연결
SELECT DISTINCT s.dept → 중복 없이 학과명만 조회
결과: 현재 수강 중인 학생들의 학과 목록이 출력됨

21번 2024년에 입학한 학생의 이름과 "admit_year + 1" 값을 NEXT_YEAR 별칭으로 출력하시오.
SELECT name, admit_year + 1 AS NEXT_YEAR → 이름과 입학년도+1을 조회하며 NEXT_YEAR라는 별칭 지정
FROM Students → 학생 테이블 조회
WHERE admit_year = 2024 → 2024년 입학 학생만 선택

22번 학생 이름을 대문자로 변환해 name_up 컬럼으로 조회하시오.
SELECT UPPER(name) AS name_up
FROM Students;
UPPER(name) → 이름을 모두 대문자로 변환
AS name_up → 변환된 컬럼에 name_up이라는 별칭 지정
FROM Students → Students 테이블에서 조회

23번 과목 title에서 앞의 3글자만 잘라 abbr로 조회하시오.
SELECT LEFT(title, 3) AS abbr
FROM Courses;
LEFT(title, 3) → 문자열의 왼쪽 3글자 추출
AS abbr → 추출한 값을 abbr라는 별칭으로 지정
FROM Courses → Courses 테이블에서 조회

24번 Kim이 수강 중인 과목의 title 목록을 조회하시오.
SELECT c.title
FROM Students s
JOIN Enroll e ON s.sid = e.sid
JOIN Courses c ON e.cid = c.cid
WHERE s.name = 'Kim';
Students s와 Enroll e를 sid 기준으로 연결 → 학생과 수강 정보를 매칭
Enroll e와 Courses c를 cid 기준으로 연결 → 수강 과목 정보 확보
WHERE s.name = 'Kim' → 이름이 Kim인 학생 필터
SELECT c.title → Kim이 수강 중인 과목 제목 조회

25번Enroll.grade가 'A'면 4, 'B'면 3, 그 외 0으로 환산하여 score 컬럼으로 조회하시오.
SELECT sid, cid,
       CASE 
           WHEN grade = 'A' THEN 4
           WHEN grade = 'B' THEN 3
           ELSE 0
       END AS score
FROM Enroll;
CASE WHEN ... THEN ... ELSE ... END → 조건별 값 반환
AS score → 계산된 점수를 score라는 별칭으로 지정
FROM Enroll → 수강 정보 테이블 조회

26번 학생 테이블에 대한 SELECT 권한을 사용자 studuser에게 부여하고, 이후 해당 권한을 회수하는 SQL을 작성하시오.
-- 1. 권한 부여
GRANT SELECT ON Students TO 'studuser'@'localhost';

-- 2. 권한 회수
REVOKE SELECT ON Students FROM 'studuser'@'localhost';

GRANT SELECT ON Students TO 'studuser'@'localhost'; → studuser에게 Students 테이블 조회 권한 부여
REVOKE SELECT ON Students FROM 'studuser'@'localhost'; → 부여된 조회 권한 회수
'localhost' 부분은 사용자가 접속하는 호스트에 맞게 변경 가능
