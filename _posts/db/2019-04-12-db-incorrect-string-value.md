---
layout: post
title: Maria DB Incorrect string value Error
categories: [db]
tags: [db,mariadb,basic]
comments: true
---

### 상황

- 회원가입 구현 중 이름에 영어를 넣으면 성공적으로 회원가입이 되지만 한글을 넣으면 회원가입 실패가 뜸.
- 서버에서 아래 에러 발생
- Incorrect string value: '\xED\x85\x8C\xEC\x8A\xA4...

~~~
[ERROR][][2019-04-12][16:35:46.145] c.a.d.m.d.controller.UserController - [exceptionHandler] [org.springframework.dao.DataIntegrityViolationException] [999] [UNKNOWN_ERROR] [
Error updating database.  Cause: java.sql.SQLDataException: (conn:19) Incorrect string value: '\xED\x85\x8C\xEC\x8A\xA4...' for column 'NAME' at row 1
Query is: INSERT INTO user
    (
            user_seq
           , id
           , password
           , name
    )
    VALUES
    (
        ?
        ,?
        ,?
        ,?
    ), parameters [<null>,'test','MDk4ZjZiY2Q0NjIxZDM3M2NhZGU0ZTgzMjYyN2I0ZjY=','테스트']
The error may involve user.createUserVO-Inline
The error occurred while setting parameters
SQL: INSERT INTO user  (    user_seq      , id      , password      , name  )  VALUES  (   ?   ,?   ,?   ,?  )
Cause: java.sql.SQLDataException: (conn:19) Incorrect string value: '\xED\x85\x8C\xEC\x8A\xA4...' for column 'NAME' at row 1
~~~

### 해결방법

- 테이블 Charset이 utf8이 아니기 때문에 변환이 실패하여 한글을 넣지 못하는 것으로 추측
- 테이블 생성 시 기본 CHARSET을 utf8로 설정해준다
- 한글 데이터가 잘 들어가는 것을 확인

~~~
CREATE TABLE `user` (
  `USER_SEQ` bigint(20) NOT NULL AUTO_INCREMENT,
  `ID` varchar(20) NOT NULL,
  `password` varchar(50) DEFAULT NULL,
  `NAME` varchar(30) DEFAULT '',
  PRIMARY KEY (`USER_SEQ`)
) ENGINE=InnoDB AUTO_INCREMENT=9 DEFAULT CHARSET=utf8
~~~