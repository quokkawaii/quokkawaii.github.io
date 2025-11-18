---
layout: post
title: "비동기 정리 25.11.18"
subtitle:
author: quokkawaii
categories: javascript
tags: javascript
top: 1
sidebar: []
---

<h2> 비동기 처리</h2>

<p> 현재 실행중인 *태스크가 실행되지 않아도 다음 태스크를 실행하는 방식을 비동기 처리라고 합니다. 해당 기능이 없다면 어떤일이 벌어지는지를 정리하기 위한 글입니다. </p>

<p> *태스크 : 컴퓨터에서 실행되는 최소 단위의 작업 </p>

<h2> 비동기 처리가 없는 함수 </h2>

``` javascript
const time = (callbackFunction, delay) => {
  const nowSecond = Date.now() + delay;

  while(Date.now() < nowSecond);

  callbackFunction();
}

const foo = () => console.log("foo");

const bar = () => console.log("bar");

time(foo, 3000);

bar();

// result  
// "foo"
// "bar"
```

<p> 해당 코드는 현재 시간 + delay를 한값(nowSecond)와 while문을 돌며 새로운 시간을 비교하여 nowSecond의 값이 더 작아질때 통과되는 코드 입니다. 만약 delay의 값이 3000이라면 3초뒤에 callbackFunction()을 실행이 됩니다. 그렇다면 해당 구조에서 bar()가 실행되는 지점은? </p>

<h2> 비동기 </h2>

<p> 기본적으로 자바스크립트 엔진은 싱글 쓰레드를 사용하고 있습니다. 싱글 쓰레드를 씀으로 한번에 하나씩의 코드를 읽을 수 밖에없기때문에 비동기 함수를 만날경우 비동기 처리 방식으로 넘깁니다. 하지만 위의 코드는 비동기가 아님으로 원래 처리하던 방식대로 처리가 됩니다, 즉 time()이 끝나는 시점에 bar()함수가 실행이 됩니다.</p>

<h2> 비동기 처리 코드 </h2>

``` javascript

const foo = () => console.log("foo");

const bar = () => console.log("bar");

setTimeout(foo, 3000);

bar();

// result
// "bar"
// "foo"
```
<p> 해당 코드는 타이머 함수입니다. 타이머 함수는 비동기 처리 방식으로 실행되기 때문에 해당 코드는 비동기 함수라고 볼 수 있습니다. 해당 코드와 비동기의 코드를 비교하자면, 똑같이 bar() 콜백함수보다 먼저 실행했지만, 비동기 처리 코드는 "bar"다음에 "foo"가 출력이 되는것을 확인할 수 있었습니다.  </p>

<p> 주의점 : setTimeout()과 setInterval()은 비동기 함수이지만, promise는 아닙니다. 즉 async/await 사용하면 안됩니다. </p>

<h2> 비동기 함수로 만들기 </h2> 

<p> 추후 업데이트 예정 </p>