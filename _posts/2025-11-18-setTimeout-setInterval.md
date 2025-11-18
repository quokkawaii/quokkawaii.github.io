---
layout: post
title: "비동기 함수 setTimeout과 setInterval"
subtitle:
author: quokkawaii
categories: javascript async setTimeout setInterval
tags: javascript async setTimeout setInterval
top: 1
sidebar: []
---

<P> 글을 작성하기 앞서 비동기에 대한 글은 해당 
  <a href ="https://quokkawaii.github.io/javascript/2025/11/18/async-function.html">링크</a>를 참조하시기 바랍니다. 
</p>

<h2> 타이머 함수 </h2>

<p> 일반적으로 타이머 함수는 일정 시간이 지난후 실행되는 함수나, 일정 시간을 기준으로 계속하여 반복하는 함수들을 말합니다. 자바스크립트에서는 setTimeout() / clearTimeout 과 setInterval() / clearInterval()이 있습니다. 해당 함수들이 각각 무슨 기능을 가지고 있는지와 정의하는 방법 등을 정리하기 위한 글입니다.</p>

<h2> setTimeout() </h2>

<p> 
  setTImeout()은 두번째 매개변수인 delay에 입력된 milliSecond 뒤에 첫번째 매개변수 functionRef를 실행합니다. 해당 과정에서 비동기 처리 방식이 적용되기 때문에 실행이 되지않은 코드가 기다리는 일은 없습니다. 
</p>

<h2> setTimeout() 호출 방법 </h2>

```javascript
setTimeout(functionRef, delay);
```

<p> 
setTimeout()에는 3번째, 4번째 등 여러 값들을 넣을 수있지만 가장 일반적인 사용법인 첫번째,두번째 매개변수로 호출하는 방법에 대해 정의해보았습니다. 다음은 이것을 활용하고 비동기 함수임을 증명하는 코드입니다.
</p>

```javascript
const foo = () => console.log("foo");

const bar = () => console.log("bar");

setTimeout(foo, 2000);

bar();

// result
// "bar"
// "foo"
```

<p> 
위의 코드는 2초뒤 foo 콜백함수를 호출하는 코드와 bar()함수를 호출하는 코드입니다. 
해당 코드가 비동기임을 증명하는 이유는, setTimeout()이 먼저 호출이 되었음에도 bar()함수가 먼저 출력이 되는것을 볼 수 있습니다.
</p>

<h2> clearTimeout() </h2>

<p> 
해당 함수는 setTimeout()가 호출된것을 취소하는 함수입니다. 처음 setTimeout()를 호출하면 리턴값으로 setTimeout() 객체의 고유 번호가 저장이 됩니다. 해당 값을 매개변수로 넘기면 해당 setTimeout()은 취소가 되는 방식입니다.  
</p>

```javascript
const foo = () => console.log("foo");

const timeId = setTimeout(foo, 2000);

clearTimeout(timeId);
```

<p> 
  코드 실행시, console에는 아무것도 출력이 되지 않음을 알 수 있습니다. 
</p>

<h2> setInterval() </h2>

<p>
 setInterval()은 특정 delay(밀리초)마다 컴파일되고 실행됩니다. setTimeout()과 마찬가지로 똑같은 매개변수를 가집니다.
</p>

<h2> setInterval() 호출 방법 </h2>

```javascript
const foo = () => console.log("foo");

const bar = () => console.log("bar");

setInterval(foo, 2000);

bar();

//result
// "bar"
// "foo"
// "foo"
// "foo" 2초마다 반복
```

<p>
 위의 주석을 보면 "2초마다 반복"이것이 setInterval()의 핵심입니다. 해당 프로그램이 끝나기 전까지 delay(밀리초)의 텀을 두고 계속해서 반복합니다. 그러면 해당 반복은 멈출 수가 없나? 그건 아닙니다. setTimeout()과 같이 고유 Id를 가지고 있으며 해당 Id를 clear해줌으로써 실행을 취소할 수 있습니다.
 </p>

<h2> clearInterval() </h2>

```javascript
let count = 1;

const foo = () => {
  console.log(`${count++}번째 foo 호출`);
  if (count > 3) cancel(intervalId);
};

const cancel = (intervalId) => clearInterval(intervalId);

const bar = () => console.log("bar");

const intervalId = setInterval(foo, 2000);

bar();

// result
// "bar"
// "1번째 foo 호출"
// "2번째 foo 호출"
// "3번째 foo 호출"
```

<h2> 코드 해석 </h2>

<p> 
  처음 setInterval()이 호출되고 그 후에 bar()이 호출됩니다. 하지만 Interval은 비동기이기 때문에 "bar"이 먼저 출력이 됩니다. 이후에는 2초 마다 반복되는 코드가 생성되지만, count의 값이 3을 넘어선다면 if문에 의해 interval의 실행을 지워줍니다. 이러한 방법으로 setInterval() 함수를 제어할 수 있습니다.
</p>

<h2> 마치며 </h2>

<p>
  보통의 비동기 함수라면 promise가 필수입니다. promise임을 알려줌으로 컴파일러가 해당 함수는 비동기임으로 비동기 처리를 해야한다를 판단할 수 있습니다. 하지만 setTimeout과 setInterval은 비동기이지만 promise가 선언되어 있지 않습니다. 해당 방법이 궁금해 검색해본 결과 nodeJs에 의해 두 함수가 비동기임을 정해뒀다고 하더군요.. 결국 중요한건 promise가 아님으로 async/await를 쓰지 않아도 된다는것입니다. 
</p>
