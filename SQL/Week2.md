# SQL_ADVANCED 2주차 정규 과제 

## Week 2 :집합 연산자 & 그룹 함수

📌**SQL_ADVANCED 정규과제**는 매주 정해진 주제에 따라 **MySQL 공식 문서 또는 한글 블로그 자료를 참고해 개념을 정리한 후, 프로그래머스/ Solvesql / LeetCode에서 SQL 3문제**와 **추가 확인문제**를 직접 풀어보며 학습하는 과제입니다. 

이번 주는 아래의 **SQL_ADVANCED_2nd_TIL**에 나열된 주제를 중심으로 개념을 학습하고, 주차별 **학습 목표**에 맞게 정리해주세요. 정리한 내용은 GitHub에 업로드한 후, **스프레드시트의 'SQL' 시트에 링크를 제출**해주세요. 



**👀 (수행 인증샷은 필수입니다.)** 

> 프로그래머스 문제를 풀고 '정답입니다' 문구를 캡쳐해서 올려주시면 됩니다. 



## SQL_ADVANCED_2nd

**1. 집합 연산자**

### 15.2.18. UNION Clause

### 15.2.14. Set Operations with UNION, INTERSECT

- UNION, UNION ALL 중심으로 개념을 정리하고, INTERSECT, EXCEPT는 구문이 어떤 기능을 하는지 간단히만 알아봅니다. EXCEPT와 INTERSECT는 대부분 MySQL 버전에서 공식 지원되지 않기 때문에, **이번주 학습은 `UNION, UNION ALL` 만 집중적으로 정리해주세요.**

**2. 그룹 함수 (집계 함수)**

### 14.19.1. Aggregate Function Descriptions



## 🏁 주차별 학습 (Study Schedule)

| 주차  | 공부 범위               | 완료 여부 |
| ----- | ----------------------- | --------- |
| 1주차 | 서브쿼리 & CTE          | ✅         |
| 2주차 | 집합 연산자 & 그룹 함수 | ✅         |
| 3주차 | 윈도우 함수             | 🍽️         |
| 4주차 | Top N 쿼리              | 🍽️         |
| 5주차 | 계층형 질의와 셀프 조인 | 🍽️         |
| 6주차 | PIVOT / UNPIVOT         | 🍽️         |
| 7주차 | 정규 표현식             | 🍽️         |



### 공식 문서 활용 팁

>  **MySQL 공식 문서는 영어로 제공되지만, 크롬 브라우저에서 공식 문서를 열고 이 페이지 번역하기에서 한국어를 선택하면 번역된 버전으로 확인할 수 있습니다. 다만, 번역본은 문맥이 어색한 부분이 종종 있으니 영어 원문과 한국어 번역본을 왔다 갔다 하며 확인하거나, 교육팀장의 정리 예시를 참고하셔도 괜찮습니다.**



# 1️⃣ 학습 내용 

> 아래의 링크를 통해 *MySQL 공식문서*로 이동하실 수 있습니다.
>
> - 15.2.18. UNION Clause : MySQL 공식문서 
>
> https://dev.mysql.com/doc/refman/8.0/en/union.html
>
> - 15.2.14. Set Operations with UNION, INTERSECT : MySQL 공식문서
>
> https://dev.mysql.com/doc/refman/8.0/en/set-operations.html
>
> (한국어 버전) https://dart-b-official.github.io/posts/mysql-UNION/
>
> - 14.19.1. Aggregate Function Descriptions : MySQL 공식문서
>
> https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html
>
> (한국어 버전) https://dart-b-official.github.io/posts/mysql-aggregate_function/



<!-- 여기까진 그대로 둬 주세요-->

# 2️⃣ 학습 내용 정리하기

## 1. 집합 연산자

~~~
✅ 학습 목표 :
* UNION과 UNION ALL의 차이와 사용법을 이해한다.
* 중복 제거 여부, 컬럼 정렬 조건 등을 고려하여 올바르게 집합 연산자를 사용할 수 있다. 
~~~

### Union Clause 
■ UNION: 두 쿼리 블록의 모든 결과를 결합하고, 중복 제거 <br>
```SELECT '사과' UNION ALL SELECT '사과'; -- 결과: 사과, 사과 ``` <br>
■ INTERSECT: 두 쿼리 블록 모두에 공통으로 존재하는 행만 반환, 중복 제거 <br>
```SELECT '사과' INTERSECT SELECT '사과'; -- 결과: 사과 ``` <br>
■ EXCEPT: 두 쿼리 블록 A, B에서 A에만 존재하고 B에는 없는 행 반환, 중복 제거 <br>
```SELECT '사과' EXCEPT SELECT '바나나'; -- 결과: 사과 ``` <br>

#### 옵션:
  - `ALL` → 중복 허용 <br>
  - `DISTINCT` → 중복 제거 (기본)

#### 우선순위
- INTERSECT는 UNION, EXCEPT보다 우선 평가
- UNION, INTERSECT는 교환법칙 성립



## 2. 그룹함수

~~~
✅ 학습 목표 :
* COUNT, SUM, AVG, MAX, MIN 함수의 기본 사용법을 익힌다.
* GROUP BY와 HAVING 절을 적절히 활용할 수 있다.
* NULL과 집계 함수가 어떻게 상호작용하는지 이해한다. 
~~~

### Aggregate Function
# MySQL 집계 함수 정리

# MySQL 집계 함수 정리

| 함수 | 기본 설명 | 상세 설명 / 특징 | 예시 |
|------|-----------|------------------|------|
| **AVG([DISTINCT] expr)** | 평균값 반환 | - DISTINCT 지정 시 중복 제외 평균<br>- 행이 없거나 NULL만 있으면 NULL<br>- `OVER` 가능 (DISTINCT와 함께는 불가) | ```sql<br>SELECT AVG(score) FROM student;<br>``` |
| **BIT_AND(expr)** | 비트 AND | - 이진 문자열/숫자 타입 지원<br>- NULL 무시 (전부 NULL → 중립값)<br>- 행이 없으면 “모든 비트=1” 반환<br>- `OVER` 가능 (8.0.12+) |  |
| **BIT_OR(expr)** | 비트 OR | - BIT_AND와 유사 규칙<br>- 행이 없으면 “모든 비트=0” 반환<br>- `OVER` 가능 (8.0.12+) |  |
| **BIT_XOR(expr)** | 비트 XOR | - BIT_AND와 유사 규칙<br>- 행이 없으면 “모든 비트=0” 반환<br>- `OVER` 가능 (8.0.12+) |  |
| **COUNT(expr)** | 행 수 반환 | - NULL 제외 행 수 반환<br>- 전부 NULL/행 없음 → 0<br>- `COUNT(NULL)`은 항상 0<br>- `COUNT(*)`는 모든 행 수<br>- `OVER` 가능 | ```sql<br>SELECT COUNT(*) FROM student;<br>``` |
| **COUNT(DISTINCT expr)** | 서로 다른 값의 개수 반환 | - 여러 컬럼 조합도 허용(MySQL 확장)<br>- NULL 제외 |  |
| **GROUP_CONCAT(expr)** | 그룹 내 문자열 연결 | - 기본 구분자 `,` (SEPARATOR로 변경 가능)<br>- 결과 길이 = `group_concat_max_len` (기본 1024)<br>- 모두 NULL → NULL | ```sql<br>SELECT GROUP_CONCAT(score) FROM student;<br>``` |
| **JSON_ARRAYAGG(expr)** | JSON 배열 집계 | - 각 행 값을 배열 요소로 변환<br>- NULL 요소는 `[null]`로 포함<br>- 행이 없으면 NULL<br>- `OVER` 가능 (8.0.14+) | ```sql<br>SELECT JSON_ARRAYAGG(attr) FROM t3;<br>``` |
| **JSON_OBJECTAGG(key, val)** | JSON 객체 집계 | - (키, 값) 쌍 집계<br>- NULL 키 → 오류<br>- 중복 키 → 마지막 값이 우선<br>- `OVER` 가능 (8.0.14+) | ```sql<br>SELECT JSON_OBJECTAGG(c, i) FROM t;<br>``` |
| **MAX([DISTINCT] expr)** | 최댓값 반환 | - NULL만 있으면 NULL<br>- 문자열/ENUM/SET 비교는 값 기준<br>- DISTINCT는 생략과 동일<br>- `OVER` 가능 (DISTINCT 불가) | ```sql<br>SELECT MAX(score) FROM student;<br>``` |
| **MIN([DISTINCT] expr)** | 최솟값 반환 | - MAX와 동일한 제약 |  |
| **STD(expr), STDDEV(expr)** | 모표준편차 | - `STDDEV_POP()` 별칭 (MySQL/Oracle 호환)<br>- NULL만 있으면 NULL<br>- `OVER` 가능 |  |
| **STDDEV_POP(expr)** | 모표준편차 | - VAR_POP()의 제곱근 |  |
| **STDDEV_SAMP(expr)** | 표본표준편차 | - VAR_SAMP()의 제곱근 |  |
| **VAR_POP(expr), VARIANCE(expr)** | 모분산 | - VARIANCE는 VAR_POP의 별칭<br>- `OVER` 가능 |  |
| **VAR_SAMP(expr)** | 표본분산 | - 분모 = N-1<br>- `OVER` 가능 |  |
| **SUM([DISTINCT] expr)** | 합계 반환 | - DISTINCT → 중복 제외 합산<br>- NULL만 있으면 NULL<br>- `OVER` 가능 (DISTINCT 불가) | ```sql<br>SELECT SUM(score) FROM student;<br>``` |

- 분산·표준편차 함수: 숫자 인자에 대해 DOUBLE 반환 <br>
- SUM(), AVG(): <br>
  - 정밀-값 인자(INTEGER, DECIMAL): DECIMAL 반환 <br>
  - 근사-값 인자(FLOAT, DOUBLE): DOUBLE 반환 <br>


<br><br>

---

# 3️⃣ 실습 문제

https://leetcode.com/problems/customers-who-never-order/

> LeetCode 183. Customers Who never Order
>
> 학습 포인트 : 주문 내역이 없는 고객을 찾기 위한 패턴 익히기  

https://leetcode.com/problems/department-highest-salary/description/

> LeetCode 184. Department Highest Salary
>
> 학습 포인트 : 부서별 최고 연봉자 추출을 위한 **그룹별 정렬 / 필터링** 방식 이해하기

---

## 문제 인증란

<!-- 이 주석을 지우고 여기에 문제 푼 인증사진을 올려주세요. -->



---

# 확인문제

## 문제 1

> **🧚동혁이는 SQL 문제를 풀면서 `UNION과 UNION ALL`의 차이를 명확히 이해하지 못해 중복된 값이 생기거나 누락되는 문제를 계속 겪고 있습니다.** 아래는 동혁이가 작성한 쿼리입니다.

~~~sql
SELECT name FROM member
UNION
SELECT name FROM blackList;
~~~

> **그런데 예상과 달리 blacklist에만 있는 이름이 결과에 안 나오거나, 중복된 이름이 사라져서 헷갈리고 있습니다. UNION과 UNION ALL의 차이를 설명하고, 중복 포함 여부에 따라 어떤 경우에 어떤 쿼리를 써야 하는지 예시와 함께 설명해주세요**

<br>

~~~
여기에 답을 작성해주세요!
~~~

## 참고자료
그룹 함수가 많아서 중요하게 많이 쓰이는 함수들을 정리해놓은 참고자료를 첨부합니다. 아래 블로그를 통해서 더욱 쉽게 공부해보시고 문제를 풀어보세요.
1. [SQL 10] 그룹 함수, GROUP BY 절, HAVING 절
https://keep-cool.tistory.com/37

또한, MySQL 문서 이외에 Oracle 함수에서 사용하는 그룹함수에 대한 소개도 같이 첨부합니다. SQLD 시험 준비하시는 분이 있다면 이 자격증 시험에서는 Oracle 언어를 기반으로 문제가 출제하오니 아래 블로그도 같이 공부해보세요. (선택사항입니다.)
2. 그룹 함수 (Group FUNCTION)
https://dkkim2318.tistory.com/48

<br>

### 🎉 수고하셨습니다.
