---
layout: post
title: "동적 라우터 만들기 (dynamic Routing)"
subtitle:
author: quokkawaii
categories: react router typescript
tags: react router typescript
top: 1
sidebar: []
---

# 동적 라우터

#### - 특정 아이템을 클릭했을시, 그 아이템만의 디테일한 정보가 나오게끔 가능하게 해줍니다.

#### - 해당 정보를 정적으로 만든다면 디테일의 정보를 전달은 가능하겠지만, 디테일 페이지가 많이 복잡해지기 때문에 동적 라우터를 사용하여 사용자가 원하는 정보만 보여 줄 수 있습니다.

## 정의

```typescript
<Route path="/movie/:id" element={<Details />} />
```

#### - 위와 같이 Route 태그안 path값에 :id를 추가해줍니다.

#### - 해당 값은 반드시 id가 아닌 다른 이름이여도 상관없습니다.

## 동적으로 :id 값 보내기

### 1. useNavigate() 사용

#### - useNavigate()는 특정 이벤트가 도달하면 매개변수로 오는 값으로 이동합니다.

#### - 해당 함수를 사용하기 위해선 import가 필요합니다.

```typescript
import { useNavigate } from "react-router-dom";

const nav = useNavigate();

// click시 이동하는 함수
const clickToMove = () => {
  // 생략
  nav(`/movie/${v.id}`);
};
```

### 2. <Link to={url}> 사용

#### - 해당 태그는 a 태그와 비슷하지만 다릅니다. a태그와 마찬가지로 url로 이동하지만, 새로고침을 하지 않습니다. 즉, 브라우저의 URL만 바꾼다고 생각하면 됩니다.

#### - 해당 태그도 사용하기 위해서 import가 필요합니다.

```typescript
import { Link } from "react-router-dom";

<Link to={`/movie/${v.id}`}>
  <img src={v.medium_cover_image} />
</Link>;
```

#### - 이런 방식으로 동적 라우터 변수에 접근할 수 있습니다.

## 동적으로 넘겨 받은 :id 값 사용하기

### - useParams() 사용하기

```typescript
import { useParams } from "react-router-dom";

let { details_id } = useParams();
```

#### - useParams안에 있는 details_id를 가져오겠다! 라는 코드입니다.

#### - {} 를 사용하지 않고 let details_id = useParams();으로 정의를 한다면 details_id안에는 다른 값들까지 들어갈 수 있으니 조심해야 합니다.

#### - 실수했었던 것인데, Route 태그의 path값에 :id로 되어 있으면 { id } = useParams() 이런 방식으로 불러와야 합니다.
