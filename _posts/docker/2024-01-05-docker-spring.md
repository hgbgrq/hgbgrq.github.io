---
title: githubAction, docker 를 이용하여 spring boot 자동으로 배포해보기
author: 형장
date: 2019-08-08 14:10:00 +0800
categories: [docker, 서버 구축]
tags: [docker]
render_with_liquid: false
---

# docker 를 이용하여 spring boot 서버 구축하기

## 해당 포스트에서 사용할 방식

- 환경
: ssh 로 접근이 가능하고 docker가 설치 되어있는 ubuntu20:04 서버
: java:17, srping boot:3.0.5 , spring-dependency-management:1.1.0, intellij
: 2024-01-12 기준 github

- 방식
: github action을 사용하여 git에 특정 brach에 push가 되면 해당 branch 를 사용하여 java 를 build 하여 jar를 만들어 ssh로 접근 가능한 
서버에 jar파일을 전송하고 그 서버에서 dockerfile로 해당 jar파일을 이용하여 컨테이너를 구축하여 배포를 진행한다.


- 실행중인 docker 컨테이너의 로그를 확인하는 방법 
```
docker logs -f gss_server
```
