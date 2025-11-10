# SQL_BASIC 6주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_6th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**6주차 과제는 강의 내용을 정리하는 것과 함께, 프로그래머스에서 제공하는 SQL 문제를 직접 풀어보는 실습도 병행합니다.** 강의에서는 **배운 내용을 정리하고 주요 쿼리 예제를 정리**하며, 프로그래머스 문제는 **직접 풀어본 뒤 풀이 과정과 결과, 배운 점을 함께 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_6th

### 섹션 6. 다량의 자료를 연결 : JOIN 

### 5-1. Intro

### 5-2. JOIN 이해하기

### 5-3. 다양한 JOIN 방법

### 5-4. JOIN 쿼리 작성하기 

### 5-5. JOIN을 처음 공부할 때 헷갈렸던 부분

### 5-6. JOIN 연습문제 1~2번

### 5-6. JOIN 연습문제 3~5번

### 5-7. 정리



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | ✅         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<!-- 여기까진 그대로 둬 주세요-->

<br>

---

# 1️⃣ 개념정리

## 5-2. JOIN 이해하기

~~~
✅ 학습 목표 :
* JOIN에 대한 정의와 필요성에 대해 설명할 수 있다.
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
Join: 2개의 테이블을 연결하는 것  
공통의 컬럼이 필요함: Key  
기준 테이블을 가지고 기준테이블에 key 컬럼을 기준으로 다른 테이블을 붙이는 것
* 붙일 수 있는 테이블 갯수 제한 X
* 조인 단계적으로 진행하면 됨
조인을 해야하는 이유: 관계형 데이터베이스 설계시 정규화 과정을 거침, 그렇기에 중복을 최소화하여 테이블을 구성하게 되기에 이후 사용 목적에 따라 조인을 하는 것
개발 관점에서는 분리되어 있는 것이 좋음.  

## 5-3. 다양한 JOIN 방법

~~~
✅ 학습 목표 :
* JOIN 방법들의 종류를 설명할 수 있다. 
* 각 JOIN 방법들의 차이점에 대해서 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
1) (Inner) Join: 두 테이블의 공통 요소만 연결
2) Left/Right (outer) join: 왼쪽/오른쪽 테이블 기준으로 연결
3) Full (outer) join: 양쪽 기준으로 연결
4) Cross join: 두 테이블 각각의 요소를 곱하기 
<img width="1344" height="650" alt="image" src="https://github.com/user-attachments/assets/240376e4-a371-49ec-8a82-32c6220c6bcc" />


## 5-4. JOIN 쿼리 작성하기 

~~~
✅ 학습 목표 :
* JOIN을 사용한 문법에 대해 이해하여 적용할 수 있다.
* JOIN 을 활용한 쿼리를 작성할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
1. 테이블 확인 : 테이블에 저장된 데이터, 컬럼 확인
2. **기준 테이블 정의** : 가장 많이 참고할 기준 테이블 정의
3. Join key 찾기: 여러 테이블과 연결할 키 정리
4. 결과 예상하기: 손, 엑셀 같은 걸로 작성
5. 쿼리 작성, 검증: 실제 실행 후 예상과 동일한지 확인해보기

'''
SELECT
 A.col1,
 A.col2,
 B.col11,
 B.col12
 FROM table1 AS A
 LEFT JOIN table2 AS B  #Leftjoin 자리에 inner, right, full join 작성 가능
 ON A.key=B.key  #키가 되는 컬럼 작성 
'''
'''
# Cross Join은 유일하게 ON이 필수로 필요하지 않음: 어차피 키가 겹치지 않아도 다 조인되기에
SELECT
 col
 FROM table_a AS A
 CROSS JOIN table_b AS B
'''

* Alias를사용할수있음, 테이블 이름이 길 수 있기 때문에 별칭(Alias)을정의해줄수있음
* 기준 테이블은 table1 이 되는 것이고, key 작성 시 table1의 키 컬럼 이름부터 작성
* id 같은 컬럼은 겹치는 경우 존재 --> 해결법: EXCEPT(id) 사용
'''
SELECT
 A.* EXCEPT(id),
 B.* EXCEPT(id)
FROM train AS A
LEFT JOIN trainer AS B
ON A.id = B.id
'''

**헷갈렸던 부분**
1. 여러 JOIN 중 어떤 것을 사용해야 할까?
  하려고 하는 작업의 목적과 예상 결과를 모두 고려하여 진행  
2. 어떤 Table을 왼쪽에 두고,어떤 Table이 오른쪽에 가야 할까?
  모든 내용이 있어야 하는 table이 무엇인지 생각해보기, 내가 풀어야 하는 문제를 명확히 파악  
3. 여러 Table을 연결할 수 있는 걸까?
  조인에 숫자 제한은 없으나, 너무 많이 하게 되면 복잡성이 너무 높아짐  
  차라리 중간 쿼리를 만들어서, 6개 --> 1개가 아니라 3개-->1개, 3개-->1개 요 형태로 나눠서 조인  
4. 컬럼은 모두 다 선택해야 할까?
어떤 데이터를 추출해서 무엇을 하고 있는지, 하고자 하는지에 따라 다름.  
사용하지 않을 컬럼은 선택하지 않는 게 빅쿼리에서 비용을 줄일 수 있음. (비용 감소 측면)  
ID 같은 경우, 유니크 측면에서 자주 사용하는 편 

## 5-6. JOIN 연습문제 1~5번 

~~~
✅ 학습 목표 :
* 연습문제(3문제 이상) 푼 것들 정리하기
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
1번 문항  
'''
답
SELECT 
 kor_name, count(tp.id) AS pokemon_cnt
 FROM (
  SELECT
  id, trainer_id, 
  pokemon_id, status
  FROM basic.trainer_pokemon
  WHERE
   status IN ("Active", "Training")
 ) AS tp
LEFT JOIN basic.pokemon as p
ON p.id = tp.pokemon_id
GROUP BY
 kor_name
ORDER BY
 pokemon_cnt DESC
 '''
2번 문항
'''
답
SELECT 
 tp.*
 p.type1
 FROM (
  SELECT
  id, trainer_id, 
  pokemon_id, status
  FROM basic.trainer_pokemon
  WHERE
   status IN ("Active", "Training")
 ) AS tp
LEFT JOIN basic.pokemon as p
ON p.id = tp.pokemon_id
WHERE
 type1 = 'Grass'
GROUP BY
 type1
ORDER BY
 pokemon_cnt DESC
 '''
 * ON 뒤에 where 조건 추가 가능

3번 문항
'''
답
SELECT
 COUNT(DISTINCT tp.trainer_id) AS trainer_uniq,
 COUNT(tp.trainer_id) AS trainer_Cnt
FROM basic.trainer as t
LEFT JOIN basic.trainer_pokemon AS tp
ON t.id = tp.trainer_id
WHERE 
 location IS NOT NULL
 AND t.hometown = tp.location 
'''
* Distinct로 겹치는 거 없애기 가능


<br>

<br>

---

# 2️⃣ 확인문제 & 문제 인증

## 프로그래머스 문제 

https://school.programmers.co.kr/learn/courses/30/lessons/164673

> 조건에 부합하는 중고거래 댓글 조회하기 (JOIN)

https://school.programmers.co.kr/learn/courses/30/lessons/144854

> 조건에 맞는 도서와 저자 리스트 출력하기 (JOIN)

<!-- 정답을 맞추게 되면, 정답입니다. 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. --> 



---

# 3️⃣ 참고자료

JOIN 에 대해서 그림으로 쉽게 이해할 수 있는 자료들도 있어서 첨부합니다. 아래의 블로그도 학습할 때 같이 참고해주세요.

1. https://data-marketing-bk.tistory.com/entry/SQL-JOIN-%ED%95%9C-%EB%B0%A9%EC%97%90-%EC%A0%95%EB%A6%AC-%EA%B0%9C%EB%85%90%EB%B6%80%ED%84%B0-%EC%BD%94%EB%93%9C%EA%B9%8C%EC%A7%80-%EC%9D%B4%EA%B2%83%EB%A7%8C-%EB%B3%B4%EC%9E%90



2. https://velog.io/@wijoonwu/JOIN

<br>

### 🎉 수고하셨습니다.
