---
layout: post
title: "리액트 초기 화면을 세팅하기"
subtitle:
author: quokkawaii
categories: coins react useEffect useState initial-value
tags: react useEffect useState initial-value
top: 1
sidebar: []
---

# 리액트의 초기 화면을 세팅하는 방법에 대하여

### - 프로젝트를 처음 빌드했을때 나오는 시작 화면에 어떤 방식으로 초기값을 넣을지 생각해 봤습니다.

### - "useState()를 사용해 초기값의 화면을 업데이트 하면된다"라고 생각 했습니다. 하지만 이는 이벤트 루프와 화면을 처리하는 방식에 대한 지식이 부족하여 할 수 있는 생각이였습니다.

### - 아래의 코드는 처음에 실행한 방법 입니다.

# useState()로 화면 UI 업데이트 하기

```typeScript

searchBit("Bitcoin");

```

### - 해당 코드는 안에 들어간 String을 기반으로 JSON 데이터에 해당 String이 있다면 coin의 정보를 가져와 useState()의 상태를 업데이트하는 함수입니다.

### - 해당 함수로 초기값을 처리하려 했으나, 화면에 UI는 나오지 않는것을 확인 할 수 있었습니다.

</hr>

# 그렇다면 useState()만으로는 화면 업데이트가 안되나?

### - useState()로 만든 코드를 더 동작해보니 **API**와 **다음 화면의 처리**는 정상적으로 동작하였습니다.

### - 이를 바탕으로 useState()는 문제가 없다는 것을 알았습니다.

# 해당 코드가 동작하지 않은 이유 ?

### - 처음 코드가 빌드될 때 JSON데이터를 저장하는 "coins"는 빈 배열입니다.

### - searcBit("Bitcoin")의 값이 해당 값을 찾을 수 없는 이유입니다.

### - 그렇기 때문에 초기 화면의 useState() 상태 업데이트는 undefined가 들어가 초기 화면에는 아무것도 나오지 않았습니다.

# 이를 해결한 방법 useEffect()

### - JSON의 데이터를 다 받고 해당 값이 변수에 저장되기까지 기다린후 화면을 처리하는 방식으로 해당 문제를 해결했습니다.

```typeScript

const [loading, setLoading] = useState<Boolean>(ture);

useEffect(() => {


  // fetch API
  ...

  setLoading(false);
  },[]);

  useEffect(() => {
    if (!loading) {
      searchBit("Bitcoin");
    }
  }, [loading]);


```

### - 코드 해석

### 1. 빌드를 시작하면 첫 번쨰 useEffect()에서 fetch API에서 JSON값을 가져옵니다.

### 2. 해당 값을 coins에 저장합니다.

### 3. 저장이 되었다면 setLoading(false)로 로딩이 끝난것을 알립니다.

### 4. 두 번째 useEffect(,[loading])에 의존성에 loading의 값이 바뀌어 해당 useEffect()가 실행이 됩니다.

### - 이런 방식으로 번거롭지만 useEffect()를 두개 사용하여 초기값을 업데이트 했습니다.
