---
layout: post
title:  "Recursive Algorithm 이해하기"
date:   2020-06-03 17:35:27 +0900
categories: Javascript
---

## Recursive Algorithm이란?
- 어떤 문제를 풀 때, 똑같은 문제를 더 작은 버전으로 만들어서 해결하는 방식.
- fucntion 속에서 스스로를 호출하는 방식으로 활용

<br/>

## Recursive function을 만들기 위해 필요한 3가지
- __A Termination Condition :__ Recursion을 끝내기 위한 조건(잘못된 상황인 경우).  
- __A Base Case :__ Recursion을 끝내기 위한 조건(원하는 값을 얻은 경우)
- __The Recursion :__ function 안에서 스스로를 호출하는 부분. 

<br/>
### ex 1) 계승값 구하기 
(출처<sup>1</sup>에서 발췌한 코드)
{% highlight javascript %} 
function factorial(x) {
  //Termination
  if (x < 0) return;

  //Base
  if (x === 0) return 1;

  //Recursion
  return x * factorial(x-1);
}

{% endhighlight %}

__factorial(3);으로 호출한 경우:__

factorial(3);
1. x가 0보다 작은가? -> 거짓 -> 계속
2. x가 0인가? -> 거짓 -> 계속
3. return 3 * factorial(2); 

factorial(2);
1. x가 0보다 작은가? -> 거짓 -> 계속
2. x가 0인가? -> 거짓 -> 계속
3. return 2 * factorial(1); 

factorial(1);
1. x가 0보다 작은가? -> 거짓 -> 계속
2. x가 0인가? -> 거짓 -> 계속
3. return 1 * factorial(0); 

factorial(0);
1. x가 0보다 작은가? -> 거짓 -> 계속
2. x가 0인가? -> 참 -> return 1; 

![recursion1](https://eungang3.github.io/sue-is-programming/assets/recursion.jpg)



<br/><br/>
출처 : <br/>
<sup>1</sup> Morelli, B. (2017, August 21). Learn and Understand Recursion in JavaScript. Retrieved June 03, 2020, from [https://codeburst.io/learn-and-understand-recursion-in-javascript-b588218e87ea](https://codeburst.io/learn-and-understand-recursion-in-javascript-b588218e87ea),<br/>
<sup>2</sup>재귀란? (개념 이해하기) | 재귀 알고리즘 | 칸아카데미. (n.d.). Retrieved June 03, 2020, from [https://ko.khanacademy.org/computing/computer-science/algorithms/recursive-algorithms/a/recursion](https://ko.khanacademy.org/computing/computer-science/algorithms/recursive-algorithms/a/recursion)