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

<h3> 문뜩 코딩을 하다가 가만히 있는 이미지를 보고 심심하다고 느껴졌습니다. 그러나 css의 애니메이션과 같은것을 공부하기에는 아직 저의 css 이해가 부족하다고 생각이 들었습니다. 그래서 생각해낸 방법이 " 타입스크립트로 n초 마다 이미지를 바꾸면 어떨까?"입니다. 해당 방법을 setInterval()로 구현을 하였으나, setTimeout()으로도 구현이 가능하다고 생각이 들어 두 비동기 함수를 비교하고자 글을 작성하게 되었습니다.</h3>

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

<p>
 해당 코드의 처음 시작지점은 movie_datas에 값이 할당이 되었을때 입니다. 그 후에는 count의 값이 변화하면 useEffect에 의해 실행이 됩니다. 그렇다면 count값을 변화 시키는것이 실행의 핵심인것을 알 수있습니다. 위의 코드의 setCount 부분이 count의 값을 변화 시키면서 (이전값 + 1) % length를 하여 count에 화면 출력할 영화 데이터 번호를 저장하는 방식입니다. 리턴값으로 호출되었던 Interval()도 지워주는 방식이기 때문에 이전 interval이 남아 있지 않습니다.
</p>

<h2> "setCount((prev) => prev + 1)"가 뭔가요?  </h2>

<p>  
  setCount() 즉, useState()가 제공하는 기능입니다. 해당 기능은 여러번 호출되어 값이 변동되는 변수들에게 항상 최신의 상태를 반영합니다. 예를 들어 count + 1로 정의하고 한번에 이 값을 업데이트 한다면 이전 값이 꼬일 수 있습니다. 하지만 해당 기능을 사용하면 항상 최신의 상태입니다.
</p>

<h2> setTimeout을 이용한 화면 전환 </h2>

```javascript
useEffect(() => {
  const foo = () => {
    setCount((prev) => (prev + 1) % movie_datas.length);
    setTimeout(() => foo, 3000);
  };

  foo();
}, [movie_datas]);
```

<p> setTimeout를 반복하여 interval처럼 사용한다고 가정했을때 해당 함수처럼 재귀적 호출로 setTimeout를 구현했습니다. 하지만 재귀 함수로 구현을 했기 때문에 메모리를 더 많이 사용하고 속도 저하도 있는것으로 알고 있습니다.  
</p>

<h2> 결론 </h2>

<p>
 처음에는 "어차피 useEffect의 의존성에 의해 반복되는것 아닌가?"라는 생각을 하게 되었고 그렇기에 "차라리 setTimeout으로 만들어보자"라는 생각을 하게 되었습니다. 하지만 생각과는 다르게 setTimeout은 재귀 함수로 만들어야 한다는점과 setInterval이 목적에 더 알맞는것을 알게되었습니다. (직관성) 
 </p>

<h2> useEffect 사용 이유? </h2>

```javascript
const countId = setInterval(() => {
  setCount((prev) => (prev + 1) % movie_datas.length);
}, 3000);
```

<p>
 해당 코드만 useEffect 밖으로 꺼내서 setInterval를 호출 했다면 어떻게 되었는지 생각해봤습니다. 일반적인 상황에선 정상적으로 돌아가겠지만, useState에 의해 컴포넌트가 랜더링 될때마다 새로운 setInterval 객체가 생깁니다. (중복)
  이와 같은 이유로 useEffect안에 정의했으며, return 값으로 clear 해줌으로써 클린업을 보장했습니다. 메모리 누수 or 중복을 막아줍니다.
 </p>
