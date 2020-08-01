---
layout: post
title:  " Javascript의 array method"
date:   2020-08-01 10:40:27 +0900
categories: Javascript
---

## 0. forEach()
- 파라미터로 콜백함수 입력, array 내 항목마다 콜백함수 적용
- arr.forEach(function(currentValue, index, arr), thisValue)

{% highlight javascript %}
const test = [1, 2, 3, 4]
test.forEach((value) => console.log(value))
// 1 2 3 4
{% endhighlight %}

<br/>

## 1. map()
- 파라미터로 콜백함수 입력, array 내 항목마다 콜백함수 적용, 콜백함수 리턴한 값으로 구성된 새 array 반환
- arr.map(function(currentValue, index, arr), thisValue)

{% highlight javascript %}
const test = [1, 2, 3, 4]
const newArr = test.map((currentValue) => {
  console.log(currentValue);
  return currentValue;
})
// 1 2 3 4
console.log(newArr) // [1, 2, 3, 4]
{% endhighlight %}

<br/>

## 2. reduce()
- array 내 항목마다 콜백함수 적용 후 단 하나의 값 반환, 콜백함수가 반환한 값을 accumulator(누산자)에 저장
- array.reduce(function(accumulator, currentValue, currentIndex, array), initialValue)

{% highlight javascript %}
const oneTwoThree = [1, 2, 3]

const result = oneTwoThree.reduce((acc, cur, i) => {
  console.log(acc, cur, i);
  return acc - cur;
}, 10);

console.log(result)
{% endhighlight %}