# SQL_BASIC 4주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_4th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**4주차 과제부터는 강의 내용을 정리하는 것과 함께, 프로그래머스에서 제공하는 SQL 문제를 직접 풀어보는 실습도 병행합니다.** 강의에서는 **배운 내용을 정리하고 주요 쿼리 예제를 정리**하며, 프로그래머스 문제는 **직접 풀어본 뒤 풀이 과정과 결과, 배운 점을 함께 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_4th

### 섹션 4. 쿼리 잘 작성하기, 쿼리 작성 템플릿 및 오류를 잘 디버깅하기

### 3-4. 오류를 잘 디버깅하는 방법



## 섹션 5. 데이터 탐색 - 변환

### 4-1. INTRO

### 4-2. 데이터 타입과 데이터 변환(CAST, SAFE_CAST)

### 4-3. 문자열 함수(CONCAT, SPLIT, REPLACE, TRIM, UPPER)

### 4-4. 날짜 및 시간 데이터 이해하기(1) (타임존, UTC, Millisecond, TIMESTAMP/DATETIME)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 3-4. 오류를 디버깅하는 방법

~~~
✅ 학습 목표 :
* 오류의 정의에 대해 설명할 수 있다. 
* 오류 메시지를 보고 디버깅이라는 과정을 수행할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
오류메세지를 통해 문제를 진단할 수 있음  
1) syntax Error(문법오류) : 에러메세지를 번역하고 해결법 찾아보기(구글, 공식문서, 챗지피티)
   - Select list must not be empty: select목록은 그 사이에 컬럼이있어야 했는데 비어있어서
   - 밑줄 앞, 뒤에 보통 문제가 있을 가능성이 농후
~~~
<ex1>
SELECT Count (id,kor_name) from basic.pokemon
-->  오류: 집계함수 count안에는 하나의 인자만 들어가야 함.
~~~
~~~
<ex2>
SELECT type1, count(id) as cnt
from basic.pokemon Group By type1

select * from basic.trainer
--> 오류: 세미 콜론 필요/ 하나의 쿼리엔 select가 1개만 있어야 함.
~~~
~~~
SELECT * from basic.trainer LIMIT 10
where id=3
--> 오류: 입력이 끝날 것으로 예상되었지만 [5:1]에서 키워드 where을 얻음
--> 즉, limit은 where뒤에 붙여줘야하는데 where앞에 와서 생기는 
~~~

## 4-2. 데이터 타입과 데이터 변환(CAST, SAFE_CAST)

~~~
✅ 학습 목표 :
* 데이터 타입의 종류를 설명할 수 있다. 
* 데이터 타입을 변환하는 방법을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
SELECT문에서도 데이터를 변환시킬 수 있다!  
데이터 타입: 숫자, 문자, 시간/날짜, 부울(Bool)

자료타입을 변경하는 함수:CAST
select cast(1 as STRING) #숫자 1을 문자 1로 변경
select cast("school" as int64) #오류 발생  
--> school은 숫자열 변환 불가
--> SAFE_CAST 사용: 변환이 실패할 경우 NULL 반환

수학함수 : 암기하지 말고, 필요할 때 찾기 
- SAFE_DIVIDE : 나누기가 안될 때, 오류가 발생하는게 아닌 null이 나옴

## 4-3. 문자열 함수(CONCAT, SPLIT, REPLACE, TRIM, UPPER)

~~~
✅ 학습 목표 :
* 문자열 함수들의 종류를 이해하고 어떠한 상황에서 사용하는지 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
**문자열 함수**
1) CONCAT: 합치기  
SELECT  
concat("안녕","하세요") as result;  
--CONCAT(컬럼1,컬럼2,...)  

2) SPLIT:나누기  
select  
split("가,나,다,라", ",") as result;  
-- split(문자열 원본, 나눌기준이 되는 문자)  

3) 문자열 자르기 : TRIM  
select  
TRIM("안녕하세요", "하세요") as result;  
-- TRIM(문자열원본, 자를단어)  

4) 영어 소문자를 대문자로 변경: UPPER  
select  
upper("abc") as result;  
--UPPER(문자열원본)  

5) 문자열 대체: REPLACE  
select  
REPLACE("안녕하세요","안녕","실천") as replace_ex  
-- REPLACE(문자열원본, 찾을 단어, 바꿀 단어)  

<실습내용>

<img width="800" height="705" alt="image" src="https://github.com/user-attachments/assets/a38ee1a8-a66c-4071-b1e3-00688e99a855" />


## 4-4. 날짜 및 시간 데이터 이해하기(1) (타임존, UTC, Millisecond, TIMESTAMP/DATETIME)

~~~
✅ 학습 목표 :
* 날짜 및 시간 데이터 타입과 UTC의 개념을 설명할 수 있다. 
* DATE, DATETIME, TIMESTAMP 에 대해서 설명할 수 있다.
* 시간함수들의 종류와 시간의 차이를 추출하는 방법을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

**날짜 및 시간 데이터 타입 파악**
- DATE, DATETIME, TIMESTAMP  
- DATE+TIME = DATETIME
- Datetime은 T가 나오고 한국 zone (Asia/Seoul) 사용 시 한국시간과 동일함. 
- TIMESTAMP: 시간 도장, UTC부터 경과한 시간을 나타내는 값(한국시간 - 9시간)
- MILLISESECOND(ms): 천분의 1초 (1000ms=1초)
- microsecond: 1/1000ms, 1/1,000,000 sec

**날짜 및 시간 데이터 관련 내용**
- GMT: 영국 그리니치 천문대 기준 시간 차이 조정하기 위한 구분선 (한국시간: GMT+9)
- 최근엔 UTC를 많이 사용: 국제적인 표준시간 (한국시간: UTC+9)

<br>

<br>

---

# 2️⃣ 확인문제 & 문제 인증

## 프로그래머스 문제 

> 조건에 맞는 회원 수 구하기 (SELECT, COUNT) 
>
> **먼저 문제를 풀고 난 이후에 확인 문제를 확인해주세요**
>
> 문제 링크 
>
> :  https://school.programmers.co.kr/learn/courses/30/lessons/131535#

<!-- 문제를 풀기 위하여 로그인이  필요합니다. -->

<!-- 정답을 맞추게 되면, 정답입니다. 라는 칸이 생성되는데 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. --> 



## 문제 1

> **🧚Q. 프로그래머스 문제를 풀던 서현이는 여러 번의 시행착오 끝에 결국 혼자 해결하기 어려워 오류 메시지를 공유하며 도움을 요청했습니다. 여러분들이 오류 메시지를 확인하고, 해당 SQL 쿼리에서 어떤 부분이 잘못되었는지 오류 메시지를 해석하고 찾아 설명해주세요.**

~~~sql
# 조건에 맞는 회원 수 구하기 (SELECT, COUNT) 
# 서현이의 SQL 첫 번째 풀이
SELECT COUNT(AGE, JOINED)
FROM USER_INFO
WHERE AGE BETWEEN 20 AND 29
  AND JOINED BETWEEN '2021-01-01' AND '2021-12-31';
  
오류 메시지 : Error: Number of arguments does not match for aggregate function COUNT
 
# 수정하고 난 이후 두 번째 풀이
SELECT AGE, COUNT(*)
FROM USER_INFO
WHERE AGE BETWEEN 20 AND 29
  AND JOINED BETWEEN '2021-01-01' AND '2021-12-31';
  
오류 메시지 : SELECT list expression references column AGE which is neither grouped nor aggregated
~~~



~~~
여기에 답을 작성해주세요!
~~~



### 🎉 수고하셨습니다.
