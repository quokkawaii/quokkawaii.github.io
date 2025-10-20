---
layout: post
title: "리액트 라우터 install"
subtitle:
author: quokkawaii
categories: react router sh bash
tags: react router sh bash
top: 1
sidebar: []
---

# 리액트 라우터란 ?

### - React의 SPA(single Page Application), URL이 바뀌어도 화면을 새로고침 하지 않고도 컴포넌트만으로 화면을 변경 가능한 기능입니다.

### - 해당 기능과 React Router를 사용하여, 특정 URL로 바뀌었을때 해당 URL에 필요한 컴포넌트를 가져와 편리하게 랜더링 가능합니다

# install

```bash

npm install react-router-dom@6

```

```yarn

yarn add react-router-dom@6

```

# import

```typescript
<Router>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/movie/:id" element={<Details />} />
  </Routes>
</Router>
```

#### - Route의 path는 URL의 주소를 넣으면 됩니다.

#### - "/"는 웰컴 페이지로 이동하는 주소입니다.

#### - /:id는 URL 주소를 동적으로 다룰때 사용합니다.

#### - element안에는 해당 주소의 메인이 될 페이지를 넣습니다.

# 내용 미흡으로 추후 추가 예정, 나중에 설치만 할 수 있게끔만..
