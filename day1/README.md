# SQL training - day 1 
```
서비스 운영 간에 필요한 간단한 DB 조회, 수정 업무에 대비해서 기초적 SQL 사용법에 대해 강의한다.
SQL 을 다뤄본 적이 없거나 간단한 SELECT * FROM TABLE 정도만 해본 사람들을 위한 초급 강의이다.
```
## DB 기본 프로그램 설치
***

### DBMS 설치

    maria db 설치
    https://offbyone.tistory.com/199

    maria db 는 mysql db 와 거의 호환된다. (같은 사람이 만들었음)
    둘다 자주 뻗는다. 무거운 쿼리를 날리지 않는 것이 좋음.

### DB Client 설치

    DBeaver 설치
    https://dbeaver.io/

    mysql workbench 를 사용하는 것도 나쁘지 않으나, 다양한 종류의 db 와 연결이 가능한 DBeaver 가 사용하기 더 편하다.

### dump 파일 import

    예제 db import

### 잘 모르는 것이 있을 때는
    https://www.w3schools.com/sql/default.asp

***

## DB 에 대한 비유
노타의 인사서류철을 관리하는 사람 

* 인사서류철 : TABLE   
* 서류 한 장 : ROW   
* 서류에 적혀있는 항목들 (이름, 나이, 전화번호 등등) : COLUMN   
* 조건에 맞는 사람의 서류를 서류철에서 선택하는 행위 : SELECT   
* 신규 입사자가 와서 새로운 서류를 서류철에 추가 : INSERT   
* 인사 정보를 바꿔야하는 경우 (예 : 미혼 -> 기혼) : UPDATE   
* 퇴사자가 발생하여 서류철에서 서류를 빼내는 행위 : DELETE   
* 서류철을 새로 만들기 : CREATE   
* 서류를 완전히 새로 만들기 위해 서류들을 모두 파기 : TRUNCATE   
* 서류철을 파기해버림 : DROP   
* 서류의 항목들을 변경 : ALTER

대체로 실제 사람의 행위 자체를 묘사하는 단어를 사용하는 것 같다.

***
## SELECT 문
서류철의 서류들 중에 조건에 맞는 서류들을 `선택`한다   

* DBeaver SQL 생성 -> SELECT
```
SELECT 
    id, 
    task_id, 
    compression_method, 
    compression_parameters, 
    is_done, 
    updated_time, 
    compression_id, 
    compressed_model_path, 
    compressed_model_profile
FROM nptk.task_detail;
```
* `*` (asterisk) 사용 -> 모든 column 
```
SELECT
    *
FROM nptk.task_detail
```
* `*` 과 column 지정을 함께 사용 가능함 (결과에 column 이름이 겹치게 되므로 바람직한 방식은 아님)
```
SELECT
    *, 
    task_id
FROM nptk.task_detail
```
* 쿼리의 결과는 다시 하나의 테이블 처럼 사용될 수 있다.
```
SELECT 
    *
FROM (
    SELECT
        *
    FROM nptk.task_detail 
) as nptk_task_detail
```


## `WHERE` 사용
```
SELECT 
    id, 
    task_id, 
    compression_method, 
    compression_parameters, 
    is_done, 
    updated_time, 
    compression_id, 
    compressed_model_path, 
    compressed_model_profile
FROM nptk.task_detail
WHERE 1=1
and id < 500;
```

## LIMIT
조회 결과의 상위 n 개 만 보여준다.   
(속도에 영향을 미치므로 대량의 데이터를 조회할 때는 반드시 이 조건을 걸어주는 것이 좋다. - 보통은 DB client 프로그램에서 자동으로 걸어줌)

```
SELECT
    *
FROM nptk.task_detail 
LIMIT 10
```
<br>

## 예제
* nptk.task_master 테이블에서 model_type 이 'keras_savedmodel' 인 데이터를 조회하시오.
* nptk.users 테이블에서 first_name, last_name, company 를 모두 입력한 데이터를 조회 하시오. (주의 : 현재 입력 받는 방식에 오류가 있어서 NULL 로 입력되어있는 row도 있고 스트링 'null' 로 입력되어 있는 row 도 있음.)
* nptk.task_master 테이블에서 task_name 에 'resnet' 이라는 문자열을 포함한 데이터를 조회하시오. (LIKE 키워드 사용 https://www.w3schools.com/sql/sql_like.asp)
  

