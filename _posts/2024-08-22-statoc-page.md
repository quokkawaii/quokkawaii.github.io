---
layout : post
title : 정적 페이지
subtitle : 예시 코드 분석
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
tags : static Spring codeAnalyze
top : 2
sidebar : []
---

### 정적 페이지
# main/resources/static 폴더에 작성하는 파일  
# 페이지의 내용이 서버에서 변경되지 않고 동일한 컨텐츠를 제공한다  
# 빠른 로딩 속도를 가지고 있어서 서버 부하가 적다  
# 하지만 동적으로 처리가 불가능함으로 보안에 취약하다  
# 입력한 코드를 그대로 웹사이트 전달해준다  
# 템플릿 엔진을 이용해 코드를 자유롭게 변경가능   

### 정적 페이지를 이용한 welcome page 구현  
## part1. welcome page란?  
# 도메인을 입력하고 들어간 사이트의 첫 화면이다  
# HTML에선 index.html을 우선적으로 찾아 그걸 welcome page로 만들어 준다  

## part2. welcome page를 화면에 출력해 보기  
# 정적으로 출력해야되기 떄문에 main/resources/static/index.html 생성  

```index.html
<!DOCTYPE HTML>
<html>
<head>
<title>hello</title>
<meta http-equiv="Content-Type" content = "text/html; charset=UTF-8" />
</head>
<body>
hello
<a href ="/hello">hello</a>
</body>
</html>
```
### 작동된 welcome page 확인  
# 1.탭의 제목 변경되었다
![](https://i.imgur.com/iy2u2bp.png) 

# 2.localhost:8080 (welcome page 화면)
![](https://i.imgur.com/YpUh5wA.png)

# 3. hello 하이퍼링크로 들어갔을때
![](https://i.imgur.com/NimKf0b.png)

### 코드 분석  
## <!DOCTYPE HTML>  
# 이 파일이 HTML5임을 알린다  
# 이걸 정의함으로 웹페이지가 표준으로 랜더링되도록 도와준다  
# 항상 최상단에 위치해야한다  

## <html>
# HTML의 모든 요소는 이 태그안에 포함한다
# 문서의 루트 요소(root element)이다 (=HTML 문서에서 최상단에 있는 요소)

## <head>
# 메타 데이터를 포함 할 수 있는 태그 (메타 데이터 = 데이터를 설명하는 데이터)
# 페이지의 제목, 스타일시트, 스크립트 등 정보를 포함 가능
# 사용자는 <head> 태그를 볼 수 없음

## <title>hello</title>
# 탭의 제목을 hello로 바꾼다 
# </tilte>은 해당 태그를 닫는것을 의미한다

## <meta http-equiv="Content-Type" content = "text/html; charset=UTF-8" />
# charset=UTF-8 -> 해당 문서가 UTF-8 인코딩을 사용함
# 대부분의 언어를 지원하는 유니코드 문자 인코딩이다
# meta http-equiv="Content-Type" -> 페이지의 문자 인코딩을 서버가 아닌 클라이언트 쪽에서 설정 가능하게한다

## </head>
# <head> 태그의 끝

## <body>
# 사용자가 실제로 볼 수 있는 모든 컨텐츠는 <body> 태그안에 정의

## Hello
# 웹 브라우저에 Hello를 띄운다

## <!--<a href = "/hello">hello</a>
# <!--<a>--> 태그는 하이퍼 링크를 생성하는 태그이다 ( 고유한 역활 )
# localhost:8080/hello 입력시 하이퍼 링크로 들어가게 된다
# hello 클릭시 마찬가지로 하이퍼 링크로 들어간다

## </body> 
# <body> 태그의 끝

## <html>
# <html> 태그의 끝

### 후기
## 정적 페이지가 무엇인지, index.html이 무슨 역활을 하는지 알았다
## 이 html의 코드를 분석함으로 조금이나마 html 문법을 이해했다



