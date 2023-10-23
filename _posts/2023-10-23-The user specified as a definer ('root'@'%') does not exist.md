---
layout: post
title: "[MySQL] The user specified as a definer ('root'@'%') does not exist"
tags: [MySQL, DB]
date: 2023-10-23 23:40
# last_modified_at: 2023-10-04 16:00

categories : [MySQL]
toc:  true
toc_label: "MySQL"
---

## Intro
> 앞 게시물 과정(비밀번호 재설정) 후 MySQL은 동작이 잘됐지만 제목과 같은 에러가 발생했고 이에 대해 기록한다. 

## The user specified as a definer ('계정명'@'호스트') does not exist
> 해당 에러는 계정명에 해당하는 유저에 권한이 설정되지 않아서 발생한 것이다.

## 해결 방법
1. 해당 사용자가 user 테이블에 존재하는 지 확인한다.
   - `use mysql`
   - `SELECT user,host FROM mysql.user;`
      ![img](https://user-images.githubusercontent.com/112313165/277371078-d1233825-9ddf-48db-89a0-9af7e171f057.png)
2. 여기서, 사용자가 없는 경우는 사용자를 생성한다. (있는 경우 3번으로!)
   - `CREATE USER '생성 유저 이름'@'%' IDENTIFIED BY '패스워드';`
3. 해당 유저에 권한을 부여한다.
   - `GRANT ALL PRIVILEGES ON *.* TO '사용자 이름'@'%' WITH GRANT OPTION;`
4. 로그인 진행

## 참고 사이트
[Error 참고 사이트](https://velog.io/@lsg6542/The-user-specified-as-a-definer-root-does-not-exist-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0)
