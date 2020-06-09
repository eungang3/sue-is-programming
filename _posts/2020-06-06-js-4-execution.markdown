---
layout: post
title:  "Javascript의 execution contexts"
date:   2020-06-06 01:40:27 +0900
categories: Javascript
---

Udemy - [The Complete JavaScript Course 2020: Build Real Projects!](https://www.udemy.com/course/the-complete-javascript-course/) 강좌의 섹션 3. How JavaScript Works Behind the Scenes와 Kyle Simpson의 책 [You don't know JS yet: Scope & Closuers](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md)를 요약한 내용입니다. 

<br/>

## 0. Execution Context(실행 컨텍스트)란?
- 코드를 실행하기 위해 필요한 환경
- JS engine이 만드는, 변수를 저장하고 코드를 실행하는 상자같은 것. 
- object(객체)의 형태를 가짐, stack 형태로 쌓임 
- Variable Object, Scope chain, "This" variable을 프로퍼티로 가짐. 

<br/>

## 1. Execution Context의 종류
### 1) Global Execution Context(GEC)
- 디폴트 환경상자, 단 하나만 존재함. 
- 코드 실행 전에 생성됨. 항상 Execution Context stack의 최하단에 위치. 
- function 밖에 있는 모든 변수, function을 저장하고 실행.


### 2) Function Execution Context(FEC)
- function body를 실행할 때 사용하는 환경상자
- function을 호출할 때마다 각 function당 하나씩 생성.

### 3) Eval Execution Context(EEC)
- eval function(js 개발에선 잘 안씀) 속 코드 실행할 때 사용하는 환경상자. 

<br/>

## 2. Execution Context Object의 Phase
### 1) Creation phase
#### a. Variable Object 생성
- Variable Object 만들고 코드 실행에 필요한 정보를 저장하는 과정. 

- GEC의 경우 : Variable object는 Global object를 가리킴. 
![js-execution2](https://eungang3.github.io/sue-is-programming/assets/js-execution2.jpg)
    + 가. Global object에 모든 function declaration을 프로퍼티로 담음. __(=hoisting)__

    + 나. Global object에 모든 variable declaration(let, const로 정의된 variable 제외)을 프로퍼티로 담고 값을 undefined로 설정. __(=hoisting)__ 

    + cf) 브라우저에서 실행 시 global object는 window. global EC에 들어가는 변수는 모두 window의 프로퍼티. (globalVariable === window.globalVariable)

- FEC의 경우 : Variable object는 Activation Object를 기리킴.
![js-execution3](https://eungang3.github.io/sue-is-programming/assets/js-execution3.jpg) 
    + 가. Activation Object 안에 Argument Object 생성하고 function에 들어간 모든 parameter, argument를 프로퍼티로 담음. 

    + 나. Activation Object에 모든 function declaration을 프로퍼티로 담음. __(=hoisting)__

    + 다. Activation Object에 모든 variable declaration(let, const로 정의된 variable 제외)을 프로퍼티로 담고 값을 undefined로 설정. __(=hoisting)__ 



<br/>

#### cf) hoisting
- function, variable을 컴파일 단계에서 메모리에 저장해서, 코드 실행 전에 사용 가능한 상태로 만들어주는 행동. function은 define된 상태로 저장, variable은 undefined된 상태로 저장하고 실행 단계에서 define함. function은 declaration되었을 때만 hoisting됨.

{% highlight javascript %}
//function declaration의 경우

sum(1, 2); // 오류없이 3 출력

function sum(a, b){
    console.log(a + b);
}
{% endhighlight %}

{% highlight javascript %}
//function expression의 경우

sum(1, 2); //Uncaught TypeError: sum is not a function 뜸

var sum = function(a, b){
    console.log(a + b);
}
{% endhighlight %}

{% highlight javascript %}
//var로 정의한 variable의 경우

console.log(num); // undefined 출력
var num = 3;
console.log(num); // 3 출력
{% endhighlight %}

{% highlight javascript %}
//GEC와 FEC에 같은 이름 갖는 variable 들어있을 떄

var num = 1; //GEC에 저장됨

function num(){
    var num = 2; //num()이 생성한 FEC에 저장됨
    console.log(num); // 2 출력
}

console.log(num); // 1 출력
{% endhighlight %}

<br/>

#### b. Scope chain 프로퍼티 생성
- Scope : 누가(ex. function) 어디(ex. variable)에 접근할 수 있는지 정해주는 것. 

- function 생성 시에만 새로운 scope 생성 (다른 언어에선 block만으로도 스코프 생성 가능)

- lexical scoping 적용됨: 어떤 function의 안에 적혀있는 function은 바깥 function의 scope도 가짐. 

- Scope chain : 현재 EC의 VO와 모든 부모의 VO의 목록 = 현재 EC가 접근할 수 있는 것들의 목록

![js-execution1](https://eungang3.github.io/sue-is-programming/assets/js-execution1.jpg)

#### c. "this" variable 프로퍼티 생성

<br/>
### 2) Execution phase
- 해당 EC를 생성한 코드를 line by line으로 실행

<br/><br/>
출처 : <br/>
<sup>1</sup>Jonas Schmedtmann. The Complete JavaScript Course 2020: Build Real Projects!. Retrieved June 06, 2020, from [https://www.udemy.com/course/the-complete-javascript-course/](https://www.udemy.com/course/the-complete-javascript-course/)<br/>

<sup>2</sup>Simpson, K. (2019). You don't know JS yet: Get Started. Sebastopol, CA: O'Reilly Media. from [https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md) <br/>

<sup>3</sup>http://davidshariff.com/blog/what-is-the-execution-context-in-javascript/ <br/>

<sup>4</sup>https://poiemaweb.com/js-execution-context <br/>