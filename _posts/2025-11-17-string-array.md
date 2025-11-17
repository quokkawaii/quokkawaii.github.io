---
layout: post
title: "API로 받은 타입이 string array일때 값 저장 방법"
subtitle:
author: quokkawaii
categories: react API JSON
tags: react API JSON
top: 1
sidebar: []
---

<h1>String Array와 API</h1>

<h3>String 타입의 데이터를 한곳에 모은 배열입니다. 해당 값을 API 데이터를 받아 저장하던중 실수로 인해 오류가 발생하여 적은 글입니다. TypeScript 환경에서 API의 값을 사용하려면 tpye를 정의하면 해당 type과 일치하는 값을 사용 할 수 있습니다. 하지만 string[]의 값을 막상 저장을 하려니 혼란이 생겼습니다.</h3>

<hr>

<h1> 실수 1 </h1>

<h3> 처음으로 한 실수는 type의 정의를 실수했습니다. API의 데이터 값이 string[]으로 되어 있었기에 string[] type으로 저장하면 되는줄 알았습니다.</h3>

```typescript
// 예시 코드
type Genres = {
  genres: string[];
};

// api에서의 구조
const data: Genres[] = [
  { genres: ["액션", "SF"] },
  { genres: ["코미디", "드라마"] },
];

const category: string[] = data.map((v) => v.genres);
// 저장되는 category의 값 [["액션","SF"],["코미디","드라마"]]
```

<h1> 문제 해결 방법  </h1>

<h3> map => flatMap()으로 바꿔 저장되는 값을 String[]으로 설정하여 해결했습니다. 하지만 다른 문제가 남아있었는데 중복값을 제거하는 과정입니다.</h3>

<h1> 실수 2 </h1>

<h3> 이번 실수는 new Set()를 사용하는 과정에서 일어났습니다. new Set()의 저장값이 객체이지만 1차원 배열인줄 알았습니다.</h3>

```typescript
// 실수 한 부분 예시 코드
const data: number[] = [1, 2, 3, 3];

const arr: number[] = new Set(data);
// arr의 값 {1,2,3} => 에러 발생
```

<h1> 문제 해결 방법 </h1>

<h3> 처음에는 해당 문제를 해결하지 못하고 처음의 코드로 돌아가 비효율적인 코드를 만들뻔 했습니다. 하지만 정답은 생각보다 가까이 있었고 저는 알고 있었습니다. 스프레드 문법을 사용하여 해당 문제를 쉽게 해결했습니다. </h3>

```typescript
const data: number[] = [1, 2, 3, 3];

const arr: number[] = [...new Set(data)];
// {1,2,3} => 1,2,3 => [1,2,3]
```
