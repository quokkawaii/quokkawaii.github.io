---
layout : post
title : 스프링 부트 3 다운그레이드
subtitle : 
author : qwer13124
categories : SpringBoot
banner :
    image : https://i.imgur.com/48AM4nJ.jpeg
    opacity : 0.618
    background : "#000"
    height : "100vh"
    min_height : "38vh"
    heading_style : "font-size: 4.25em; font-weight: bold; text-decoration: underline"
    subheading_style: "color: gold"
tags : test Spring prtfolio
top : 1
sidebar : []
---

### 스프링 부트 다운그레이드를 하는 이유?

# 원치않은 자동업데이트 혹은 2.x.x 버전 사용 필요 등 호환성과 문법적 차이로 인해 다운그레이드가 필요함  
# 3.x.x 버전은 JDK17이상만 사용 가능하며 2.x.x 버전은 JDK11로 하는게 맞는거 같다  
# *인텔리제이, gradle기준으로 작성했다!  


### jdk11 적용 방법  
## java_home의 JDK 버전과 파일위치 편집  
# * <주의점>   

# jdk11이 깔려있고 path값에 넣어놨을 경우 -> cmd java -version -> jdk11이 나옴  
# java_home값을 편집해야함!!  

## part1 java_home 찾기  
# <윈도우 기준> 윈도우키 -> 시스템 환경 변수 편집 -> 환경 변수 -> 시스템 변수(s)에 java_home 찾기  
# 1.java_home을 찾았다면 값을 확인 해보기   
# ![](https://imgur.com/HXbUi9O)  

# 2. 위의 사진처럼 되어있지 않거나, 버전이 다른 경우 jdk11버전을 다운받아야함 (다운방법은 패스)  
## part2 jdk11 경로 설정  
# 1. jdk11 경로 찾기, 보통 아무것도 건드리지 않고 다운받았을때 C:\Program Files\java\jdk-11 이경로에 저장된다  
# 2. java_home 두번 클릭 또는 한번 클릭후 편집을 누른다  
# 3. 변수 값(V)에 jdk11의 경로를 입력  
# 4. 모든 창 확인을 누르면 끝  
# (참고 사진)  
# ![](https://imgur.com/hFzgxsH)  

### 스프링 부트 다운그레이드를 하는 방법
## part1 bulid.gradle
# 기본적으로 3.x.x 버전은 jdk17이상만 지원하기 때문에 jdk11를 쓰기 위해서는 스프링 부트의 버전을 낮춰야한다   
# bulid.gradle 파일의 plugins부분을 수정하면 된다  

# <수정전>  

```bulid.gradle  
plugins {  
	id 'java'  
	id 'org.springframework.boot' version '3.x.x'  
	id 'io.spring.dependency-management' version '1.1.6'  
}  

```  
# <수정후>  

```bulid.gradle  
plugins {  
	id 'java'  
	id 'org.springframework.boot' version '2.7.5'  
	id 'io.spring.dependency-management' version '1.1.6'  
}  
  
 ```  

## part2 프로젝트에 jdk11 적용하기  
# 프로젝트의 메인 폴더 즉, 맨 상단에 위치한 폴더의 설정을 바꾸면 된다  
# 1.아래 사진에 보이는 helloSpring이 맨 상단에 위치한 폴더  
# ![](https://imgur.com/K67sEQi)  

# 3.우클릭후 open Module settings 클릭  
# ![](https://imgur.com/r8TRXkL)  
  
# 4.Dependencles의 Module SDK를 수정 (JDK11다운로드 받았다면 있을것이다)  
# ![](https://imgur.com/hauwTp8)  




