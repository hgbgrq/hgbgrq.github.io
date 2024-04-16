---
title: docker 를 이용하여 mysql db 구축하기
author: 형장
date: 2024-04-15 00:00:00 +0800
categories: [docker, 서버 구축]
tags: [docker]
render_with_liquid: false
---

# docker 를 이용하여 mysql DB 구축하기

1. docker 를 이용하여 구축할 mysql image를 받아 온다.
~~~
docker images --> 현재 내가 가지고 있는 docker image 를 확인
docker pull mysql --> mysql 중 가장 최신 버전의 image를 가져온다.
docker run --rm mysql:latest mysql --version --> 내가 가지고 온 image의 버전을 확인하고 싶을 때
docker pull mysql:8.3.0 --> mysql 중 8.3.0의 버전을 지정해서 가져온다.
~~~
![img01](/assets/img/post/2024051501.png)

2. 가지온 docker image 를 사용하여 docker container 를 만든다.
~~~
docker run --name mysql-hgb -v ~/hgb/gss-hrm/db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=1234 -d -p 13306:3306 mysql:latest
docker ps
~~~

- `--name mysql-hgb` - docker container 의 이름을 지정하는 옵션, 해당 옵션은 필수 사항은 아니다.
- `-v ~/hgb/gss-hrm/db:/var/lib/mysql` - docker container 중간에 작동을 멈추면 container 에서 사용했던 데이터를 기록하지 않고 날린다. 해당 명령어는 컨테이너의 /var/lib/mysql 경로에 있는 데이터들을
내 pc의 ~/hgb/gss-hrm/db 로 싱크를 해놓는 옵션이다. 즉 container 가 중간에 작동을 멈춰도 local 에는 데이터가 남아 있을 수 있게 된다.
- `-e MYSQL_ROOT_PASSWORD=1234` - mysql에서 사용하는 root 계정을 비밀번호를 정하는 옵션이다. 해당 명령어는 1234로 되어있는 비밀번호가 1234이다.
- `-d` - 해당 container 가 background 에서도 작동 할 수 있게 해주는 명령어 이다.
- `-p 13306:3306` - docker container 에서 사용되는 포트를 host에서 다르게 접근할 수 있게해주는 포트포워딩 설정 옵션이다. container 에서 사용되는 3306 port 를 localhost 에서는 13306으로 접근 할 수 있게해준다.

![img02](/assets/img/post/2024051502.png)

3. 만들어진 container 에 접속해 보기
~~~
docker exec -it mysql-hgb bash --> 지금 내가 올려놓은 container bash에 접근
mysql -u root -p --> container에 접근후 설치된 mysql에 root계정으로 접속 비밀번호는 MYSQL_ROOT_PASSWORD=1234 이므로 1234 
~~~

![img03](/assets/img/post/2024051503.png)
