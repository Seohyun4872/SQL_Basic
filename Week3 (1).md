# SQL_BASIC 3주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_3rd_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**3주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **7 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 3문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_3rd

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-6. 연습문제 1~3번

### 2-6. 연습문제 7~9번

### 2-6. 연습문제 10~12번

### 2-6. 연습문제 13~17번

### 2-7. 정리 

### 2-8. 새로운 집계함수



## 섹션 4. 쿼리 잘 작성하기, 쿼리 작성 템플릿 및 오류를 잘 디버깅하기

### 3-1. INTRO

### 3-2. SQL 쿼리 작성하는 흐름

### 3-3. 쿼리 작성 템플릿과 생산성 도구 



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | 🍽️         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 2-6. 연습문제

~~~
✅ 학습 목표 :
* 연습문제(7문제 이상) 푼 것들 정리하기
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
**1번문제: 포켓몬 중에 type2가 없는 포켓몬의 수를 작성하는 쿼리**
select 
count(id) as cnt
 from basic.pokemon
where type2 is null  
배운점: 맞음, isnull사용법을 배움

**2번문제: type2가 없는 포켓몬의 type1과 type1의 포켓몬 수를 알려주는 쿼리를 작성해주세요. 단 type1의 포켓몬 수가 큰 순으로 정렬해주세요.**  
~~~
select 
sum(id) as A, type1
 from basic.pokemon
where type2 is null 
group by type1
order by A desc  
--> 정답  
select 
count(id) as pokemon_cnt, type1
 from basic.pokemon
where type2 is null 
group by type1
order by pokemon_cnt desc
~~~
배운점:집계함수를 사용해야 하므로 groupby를 사용해야 한다는 점과 sum이 아닌 count()를 사용하는 게 해당 문제에 더 잘 맞는다는 것을 배웠다.  

**3번문제: type2 상관없이 type1의 포켓몬 수를 알 수 있는 쿼리를 작성해주세요.**  
~~~
select 
count(id) as A, type1
 from basic.pokemon
group by type1
order by A desc
--> 정답
select 
count(id) as pokemon_cnt, type1  #아니면 count(DISTINCT id) 사용 가능
 from basic.pokemon
group by type1
order by A desc
~~~
배운점: distinct는 고유한 값만 보고 싶을 때 사용한다.  

**4번문제: 전설여부에 따른 포켓몬 수를 알 수 있는 쿼리를 작성해주세요**  
~~~
select 
count(id) as pokemon_cnt, is_legendary
 from basic.pokemon
group by is_legendary
~~~
배운점: 맞음, 컬럼 이름이 길 경우 1,2,3 등으로 대체해서 사용 가능하다. 결과를 빠르게 보고 싶을 때 유용함.  

**5번문제: 동명이인이 있는 이름은 무엇일까요? (한번에 찾으려고 하지 않고 단계적으로 가도 괜찮아요)**  
~~~
select 
count(name) as cnt, name
from basic.trainer
group by name
having cnt >=2
~~~

~~~
서브쿼리 활용해서 푸는 경우
Select * from
( select name, count(name) as cnt from basic.trainer Group by name)
where cnt >= 2
~~~
배운 점: 맞춤, having 대신 서브쿼리를 활용해서 푸는 법을 생각해볼 수 있었다.  

**6번문제: trainer 테이블에서 "Iris"트레이너의 정보를 알 수 있는 쿼리를 작성해주세요**  
~~~
select 
* 
from basic.trainer
where name = "Iris"
~~~

**7번문제: trainer 테이블에서 "Iris","Whitney", "Cynthia" 트레이너의 정보를 알 수 있는 쿼리를 작성해주세요**  
~~~
select 
* 
from basic.trainer
where name in ("Iris","Whitney", "Cynthia")
~~~
배운점: OR을 써도 되지만, in 함수를 통해 더 간결하게 쿼리를 구성할 수 있다는 것을 알게 되었. 


## 2-8. 새로운 집계함수

~~~
✅ 학습 목표 :
* SQL 쿼리 구조를 이해할 수 있다. 
* SELECT, FROM, WHERE을 활용하는 방법을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

**GROUP BY ALL 사용 가능**  
기존이었다면, 앞에서 컬럼이 추가되면 Group by에도 컬럼을 추가시켜줬어야 했는데  
group by all을 활용하면 추가하지 않더라도 자동으로 앞에 언급한 컬럼들을 바탕으로 그룹화시켜줌.  

## 3-2. 쿼리를 작성하는 흐름

~~~
✅ 학습 목표 :
* 쿼리를 작성하는 흐름을 설명할 수 있다.
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->



## 3-3. 쿼리 작성 템플릿과 생산성 도구

~~~
✅ 학습 목표 :
* 생산성 도구를 만들 수 있다.
~~~

<!-- 이어질 주차에서 생산성 도구를 활용한 실습이 있습니다.강의에 맞게 제작하여 화면을 캡쳐하여 이 주석을 지우고 올려주세요. -->
**쿼리 작성 템플릿**  
~~~
쿼리를 작성하는 목표, 확인할 지표
쿼리 계산방법
데이터의 기간
사용할 테이블
조인키
데이터 특징
~~~

> 생산성도구: Espanso - 특정단어를 입력하면 원하는 문장으로 변경 가능  


<br>
<br>

---

# 2️⃣ 학습 인증란

<!-- 
<img width="1000" height="500" alt="image" src="https://github.com/user-attachments/assets/ad5bb9de-83e2-4a5c-97a8-ca0d3142f393" />

<img width="1000" height="500" alt="image" src="https://github.com/user-attachments/assets/e3a33c50-1ad2-4452-88c8-78ad79ff5004" />

<img width="1000" height="500" alt="image" src="https://github.com/user-attachments/assets/7165bcdb-6191-43be-a0f8-afe5715df93c" />

-->



<br><br>



---

# 3️⃣ 확인문제

## 문제 1

> **🧚Q. 포켓몬 게임에 재미를 느낀 동혁은 포켓몬 도감에서 강력한 포켓몬 타입을 미리 선점하기 위해, 먼저 어떤 포켓몬들이 있는지 포켓몬 수를 기준으로 내림차순 정렬하여  확인하고자 했습니다.**
>
> 그래서 다음과 같은 필요한 정보를 미리 정리해보았습니다. 

~~~
조건 : type2는 상관없이
보고 싶은 컬럼 : type1
집계 내용 : 각 type1 별 포켓몬 수
정렬 기준 : 포켓몬 수를 기준으로 내림차순 정렬
~~~

> **이 목표를 바탕으로 동혁이 아래와 같은 쿼리를 잘 작성했지만, 일부 SQL 문법 요소를 빼먹었습니다. 비어 있는 부분인 ㄱ,ㄴ,ㄷ 에 들어갈 알맞은 SQL 구문을 채워보세요:**

~~~sql
SELECT type1, (ㄱ)
FROM pokemon
(ㄴ) type1
ORDER BY (ㄱ) (ㄷ);
~~~

~~~
ㄱ: count(id) as pokemon_num
ㄴ: GROUP BY
ㄷ: desc
~~~



### 🎉 수고하셨습니다.
