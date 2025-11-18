---
layout: post
title: "리액트에서 SetInterVal()로 화면 전환 동적으로 만들기 + setTimeout()과 비교"
subtitle:
author: quokkawaii
categories: react typescript
tags: react typescript
top: 1
sidebar: []
---

<h1> 화면 전환 </h1>

<h3> 문뜩 코딩을 하다가 가만히 있는 이미지를 보고 심심하다고 느껴졌습니다. 그러나 css의 애니메이션과 같은것을 공부하기에는 css에 대한 이해도가 낮았습니다. 그래서 생각해낸 방법이 "타입스크립트로 n초 마다 이미지를 바꾸면 어떨까?"입니다. 해당 방법을 setInterval()로 구현을 하였으나, setTimeout()으로도 구현이 가능하다고 생각이 들어 두 비동기 함수를 비교하고자 글을 작성하게 되었습니다. setInterval()과 setTimeout()은 다른 글에서 정리하겠습니다. </h3>

<h1> setInterval()이란? </h1>

<h3> setInterval()은 첫번째 매개변수로 callback function을 받고, 두번째로는 millisecond를 입력 받습니다. 입력받은 콜백 함수를 millisecond 초마다 해당 함수를 실행합니다. </h3>

<h1> setInterval()을 이용한 화면 전환 </h1>

```typescript
useEffect(() => {
  // if (movie_datas.length === 0) return; 가독성 해침으로 주석처리

  const countId = setInterval(() => {
    setCount((prev) => (prev + 1) % movie_datas.length);
  }, 3000);

  return () => clearInterval(countId);
}, [movie_datas, count]);
```

<h3> 해당 코드 해석 </h3>

<h3> 추후 작성 예정  </h3>

<h3> 주의 사항 : setInterval()은 한번 실행하면 이벤트에 등록되어 clearInterval()을 호출하기 전까지 남아있습니다. 반드시 삭제해야합니다. + setInterval()은 promise가 아니다!! </h3>
