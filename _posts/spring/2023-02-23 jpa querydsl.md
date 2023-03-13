---
title: "querydsl"
excerpt: ""

categorise:
  - Blog
tags:
  - Blog
---

# querydsl


# 사용방법
spring 3.0 으로 넘어 오면서 querydsl을 사용하는 방법이 달라졌다
```gradle
  implementation 'com.querydsl:querydsl-jpa:5.0.0:jakarta'
	annotationProcessor "com.querydsl:querydsl-apt:${dependencyManagement.importedProperties['querydsl.version']}:jakarta"
	annotationProcessor "jakarta.annotation:jakarta.annotation-api"
	annotationProcessor "jakarta.persistence:jakarta.persistence-api"
```
