---
layout: post
title: "[MySQL] ERROR! The server quit without updating PID"
tags: [MySQL, DB]
date: 2023-10-18 23:00
# last_modified_at: 2023-10-04 16:00

categories : [MySQL]
toc:  true
toc_label: "DB"
---

## Intro
> 예전 프로젝트 sql 파일을 local로 연결을 하다가 mysql을 재설치하였다. 재설치 한 후에 발생하는 에러에 대해서 기록한다. 

homebrew로 삭제 및 재설치를 진행하며, M2 Mac 사용 기준입니다.(디렉토리가 다를 수 있으니 경로를 확인하시길 바랍니다.)
<span style ="color:#1E90FF">(작성자의 경로: /opt/homebrew/var/mysql)</span>

처음에 mysql을 재설치 해야겠다는 생각이 들어서 ```brew install mysql``` 을 진행 했는데 이후 워크벤치와 연결이 끊기게 되고 엄청나게 헤맸다.<br>

```mysql.server start```를 할 때마다 <span style ="color:#FF6347">"ERROR! The server quit without updating PID file (/opt/homebrew/var/mysql/사용자컴퓨터이름.pid)"</span> 에러가 발생했다.<br>

다른 사람들은 재설치를 하면 된다고 해서 재설치를 진행했으나, 해결한 후 다시 살펴보니 <span style ="color:#FF6347">기존의 파일과 PID를 깔끔하게 지우지 않아서 많이 헤맸다는 결론이 나왔다.</span><br>

## 에러 정리()
1. "ERROR! The server quit without updating PID file (/usr/local/var/mysql/사용자컴퓨터이름.pid)" 
2. ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)

첫 번째 에러의 경우는 mysql.server start를 했을 때 발생한 에러, 두 번째는 mysql -u root를 할 때 발생한 에러이다.
두 번째 에러는 첫 번째 에러를 해결하고 서버를 시작한 후로는 뜨지 않았다.
<span style ="color:#1E90FF">원인은 해당 인스턴스가 종료가 안되어서 오류가 발생한 것으로 파악된다.</span>


## 해결 방법
### mysql 삭제 과정
1. 서비스 중지
   - ```brew services stop mysql```
2. 디렉토리 삭제
   - ```rm -rf /opt/homebrew/var/mysql```
   - ```brew uninstall mysql``` (이 명령어 대신 rm -rf /opt/homebrew/Cellar/mysql를 사용할 수 있음.)
3. PID 제거
   - ```ps -ef | grep mysql``` (mysql에 관련된 프로세스 찾기, pid를 여기서 찾아서 kill 하면 된다.)
   - ```kill -9 pid```
4. ```brew list```를 통해 mysql이 잘 지워졌는 지 확인. 
   - 만약 위 작업을 진행했는데도 불구하고 남아 있다면 mysql 관련 디렉토리를 다시 찾아서 삭제해야 함.

### mysql 재설치
1. mysql 재설치
   - ```brew install mysql ```
     - 만약, <span style ="color:#FF6347">Error: No such file or directory - /usr/local/var/homebrew/linked/mysql</span> 이러한 에러가 발생할 경우
       - ```cd /usr/local/var/homebrew/linked/```
       - ```rm -rf mysql```
  
2. mysql 시작
   - ```mysql.server start```
     - ![img](https://user-images.githubusercontent.com/112313165/276261303-cd3cf12d-c3c9-43b3-9a8d-8abccf683652.png)
     - 만약 에러가 뜨지 않고 위 화면이 뜬다면 다행이다. 하지만 <span style ="color:#FF6347">ERROR! The server quit without updating PID에러가 발생한다면 아래와 같이 해결하자.</span>
   - PID 제거
     - 위 삭제과정에서 했던 것과 같이 진행한다.
     - ```ps -ef | grep mysql```
     - ```kill -9 pid```
   - mysql 소유자 확인 및 권한 변경
     - ```ls -laF /usr/local/mysql```
     - ```sudo chown -R mysql /opt/homebrew/var/mysql```
     - ```sudo chmod 777 /usr/local/mysql```
     - ```mysql.server start```


3. 성공 화면
![img](https://user-images.githubusercontent.com/112313165/276261303-cd3cf12d-c3c9-43b3-9a8d-8abccf683652.png)

혹여나 하단과 같이 “A mysqld process already exists” 가 뜬다면 해당 mysql 인스턴스가 이미 있기 때문이기에 mysql.server stop 후에 다시 mysql.server start를 해주면 된다.
![img](https://user-images.githubusercontent.com/112313165/276263744-512b1e7d-b651-4ea1-92cc-72ced78b02fa.png)




     
## 회고
섣부르게 프로그램을 지웠다가 깔려고 하지말고, 에러에 대한 블로그들을 차분히 살펴보고 진행하자.
대부분 스택오버플로우에 정보가 있었다. 스택오버플로우도 영어더라도 찾아보도록 하자.

## 참고 사이트
[PID 해결 방법1](https://antstudy.tistory.com/507)
[PID 해결 방법2](https://m.blog.naver.com/playhoos/221505255355)
[stackoverflow 참고 게시물](https://stackoverflow.com/questions/33390936/mysql-wont-shutdown-stop-server-error-mysql-server-pid-file-could-not-be-fo)
[brew install 실패 참고 사이트](https://penguin-kim.tistory.com/41)

