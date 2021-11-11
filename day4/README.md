# SQL training - day 4 : DML

## 복습
   * 여러가지 JOIN 방법들
***

## DML : Data Manipulation Language
```
데이터를 조작하는 쿼리문들
Select, Insert, Update, Delete
```
***
## INSERT INTO
```
INSERT INTO nptk.task_master
    (user_id, 
    task_id, 
    model_type, 
    model_path, 
    task_name,
    framework
    )
VALUES
    ('asdf',
    'asdf',
    'asdf',
    'asdf',
    'asdf',
    'asdf')
```
쿼리한 내용을 그대로 INSERT 하는 것도 가능하다.
```
INSERT INTO nptk.task_detail_copy 
    SELECT 
        * 
    FROM nptk.task_detail
```

***
## UPDATE SET
```
UPDATE nptk.users 
SET credit =
    CASE WHEN email like '%nota.ai'
        THEN 100000
        ELSE 200
    END
```
***
## DELETE
```
DELETE 
FROM nptk.task_master
WHERE user_id = 'asdf'
```
DELETE 를 하기 전에는 꼭 SELECT 를 찍어보는 습관을 기르자.
(SELECT 에 나온 내용과 동일한 내용이 삭제된다.)

***
## CASE WHEN
```
SELECT
	user_id, 
    credit,
	CASE WHEN credit > 10000
	    THEN 'rich'
	    WHEN credit < 10000
	    THEN 'poor'
	END
FROM nptk.users
```
***
## 예제
* users 테이블에 새로운 회원 1인을 추가하라 (내용은 아무렇게나 해도 됨)
* task_detail 테이블에서 is_done 이 1 인 row 를 삭제하라
* task_master 테이블에서 task 를 각 유저 별로 가장 최근에 생성한 하나만 남기고 is_active 를 0으로 수정하라
* users 테이블에서 email 주소 뒷 부분이 nota.ai 인 경우에는 authority 를 'admin' 으로 수정하고 나머지의 경우에는 authority 를 'customer' 로 수정하라

