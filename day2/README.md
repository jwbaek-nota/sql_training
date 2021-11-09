# SQL training - day 2 : 조회

## 복습
1. 데이터의 조회 SELECT -> 서류철의 서류 중 조건에 맞는 것을 `선택` 한다.
2. 데이터의 조건 WHERE
   
## 자주 사용되는 함수들
https://mariadb.com/kb/en/function-and-operator-reference/
### `COUNT`
```
SELECT
    COUNT(*) as cnt
FROM nptk.users
```
### `SUM`
```
SELECT
    SUM(compression_count) as su
FROM nptk.users
```
### `MAX`
```
SELECT
    MAX(compression_count) as ma
FROM nptk.users
```
### `MIN`
```
SELECT
    MIN(compression_count) as mi
FROM nptk.users
```
### `AVG`
```
SELECT
    AVG(compression_count) as av
FROM nptk.users
```
##### 여기까지 집계함수
--- 
### TIME_STAMP
### FROM_UNIXTIME
### ROW_NUMBER <- 자주 사용됨 
기타 등등 엄청 많은데 인터넷에 찾아보면 잘 나옴

----
<br>

## ORDER BY
조회 결과에 순서를 어떻게 매길 것인지를 결정한다.   
ORDER BY 를 사용해서 조회하지 않은 경우, 조회 결과에 순서가 없다고 간주해야 한다.    
(특히 DB 가 분산처리를 하는 경우 조회 할 때마다 순서가 다르게 나오는 경우가 많이 있다.)   
ORDER BY 를 사용하면 처리 속도가 느려지는 경우가 많다. INDEX 걸려있는 COLUMN 에 적용시키는 것이 좋다.

```
SELECT 
    *
FROM nptk.task_master
ORDER BY created_time (DESC)
```
* (DESC 는 역순)
<br>
<br>

## DISTINCT
중복 ROW 들을 제거한다.
```
SELECT
    DISTINCT task_id
FROM nptk.task_detail
```
자주 사용되는 조합
```
SELECT
    COUNT(DISTINCT task_id) as cnt
FROM nptk.task_detail
```

## GROUP BY
집계함수와 함께 사용하여 GROUP BY 에서 지정한 컬럼을 기준으로 집계함수를 적용한다.
```
SELECT
    task_id, COUNT(*) as cnt
FROM nptk.task_detail
GROUP BY task_id
```

## ROW_NUMBER OVER (PARTITION BY {COLUMN} ORDER BY COLUMN)
```
SELECT
    user_id, 
    task_id, 
    ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY created_time) as rn
FROM nptk.task_master
```


## 예제
* 한 번 이상 task 를 생성시킨 user_id 의 수를 구하시오.
* user_id 별로 task 를 몇 개 씩 생성시켰는지 조회하되, 가장 최근에 task 를 생성시킨 user_id 순으로 정렬하여 조회하시오.
* 가장 최근에 compression 을 수행한 사람의 email 주소는? (task_detail 의 is_done이 1 이면 compression 을 수행한 것)
* 각 유저가 `두번째` 로 생성한 task_master 의 row 들을 조회하시오.
