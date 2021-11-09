# SQL training - day 2 : 조회

## 복습
1. 데이터의 조회 SELECT -> 서류철의 서류 중 조건에 맞는 것을 `선택` 한다.
2. 데이터의 조건 WHERE
   
## 자주 사용되는 함수들
### `COUNT`
```
SELECT
    COUNT(*)
FROM nptk.users
```
### `SUM`
```
SELECT
    SUM(compression_count)
FROM nptk.users
```
### `MAX`
```
SELECT
    MAX(compression_count)
FROM nptk.users
```
### `MIN`
```
SELECT
    MIN(compression_count)
FROM nptk.users
```
### `AVG`
```
SELECT
    AVG(compression_count)
FROM nptk.users
```
##### 여기까지 집계함수
--- 
### TIME_STAMP
### FROM_UNIXTIME
### ROW_NUMBER
기타 등등 엄청 많은데 인터넷에 찾아보면 잘 나옴

----
<br>

## ORDER BY
조회 결과에 순서를 어떻게 매길 것인지를 결정한다.   
ORDER BY 를 사용해서 조회하지 않은 경우, 조회 결과에 순서가 없다고 간주해야 한다.    
(특히 DB 가 분산처리를 하는 경우 조회 할 때마다 순서가 다른게 나오는 경우가 많이 있다.)   
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
<br>

## DISTINCT
중복 ROW 들을 제거한다.
```
SELECT
    distinct user_id
FROM nptk.task_master
```
DISTINCT 를 자주 사용하게 되는 예시
```
SELECT
    count(distinct user_id)
FROM nptk.task_master
```

