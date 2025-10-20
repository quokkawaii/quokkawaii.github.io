---
layout: post
title: "sh: vite: command not found"
subtitle:
author: quokkawaii
categories: bug error
tags: react vite global error bug
top: 1
sidebar: []
---

# 에러 발생

### 해당 버그는 리액트를 처음 빌드 했을 때 나온 에러입니다.

```sh

sh: vite: command not found

```

# 에러 발생 이유

### - 해당 에러는 vite가 전역으로 설치되지 않았기 때문에 발생한 에러입니다.

# 에러 해결 방법

```sh

npm install -g vite

```

### - 위의 명령어를 입력하여 전역에 vite를 설치하여 에러를 해결했습니다.
