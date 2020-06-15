---
layout: post
title:  "Javascript Functions"
date:   2020-06-13 01:40:27 +0900
categories: Javascript
---

Udemy - [The Complete JavaScript Course 2020: Build Real Projects!](https://www.udemy.com/course/the-complete-javascript-course/) 강좌의 섹션 5. Advanced JavaScript: Objects and Functions를 요약한 내용입니다.

## 0. First class function
- js는 first-class function 지원(=function을 다른 variable과 똑같이 취급함)
    + function은 object type의 instance(=function도 object). 
    + variable에 저장 가능
    + 다른 function의 인자로 넣을 수 있음.
    + function이 function을 return할 수도 있음.

<br/>

### 1) function을 다른 function의 인자로 넣기
- callback function : 다른 function의 인자로 들어간 function.
{% highlight javascript %}
//참조 1에서 발췌한 코드

var years = [1990, 1965, 1937, 2005, 1998];

function arrayCalc(arr, fn){
    var arrRes = [];
    for (var i = 0; i < arr.length; i++>){
        arrRes.push(fn(arr[i]));
    }
    return arrRes;
}

function calculateAge(el) {
    return 2016 - el;
}

arrayCalc(years, calculateAge);

{% endhighlight %}

<br/>

### 2) function에서 function을 return하기
{% highlight javascript %}
function speak(animal){
    if (animal === 'dog'){
        return function(name){
            console.log(name + ' is barking');
        }
    } else {
        return function(name){
            console.log(name + ' is meowing');
        }
    }
}

var dogSpeak= speak('dog');
dogSpeak('Snoopy'); //snoopy is barking

speak('cat')('Garfield'); //Garfield is meowing
{% endhighlight %}

<br/>

### 3) Immediately Invoked Function Expressions(IIFE)
- 즉시실행함수. 정의하자마자 호출되는 function. 

- Self-Executing Anonymous Function이라고도 함. 

- function 바깥에서 function 내부에 접근할 수 없게 해서 data privacy 지키려고 사용.

- 한 번만 쓸 목적으로 만드는 Anonymous function 

- function declaration의 단점 보완

- function declaration의 단점  
    + global scope 오염 -> name collision 발생 가능
    + 단 한 번만 실행할 목적으로 쓰기 곤란(실수로 한 번 이상 사용하기 쉬움) 

- ()로 감싸야 함 : 
    + declaration 형태인데 함수명을 안 쓰면 오류로 처리됨.
    + ()로 감싸면 parser가 declaration이 아니고 expression으로 처리. 
    + js에서 괄호 안에 든 것은 statement가 아니라는 규칙 있기 때문. 

{% highlight javascript %}
//참조 1에서 발췌한 코드
(function (){
    var score = Math.random() * 10;
    console.log(score >= 5)
})

{% endhighlight %}

#### cf) statement(선언식) VS expression(표현식)


<br/><br/>
출처 : <br/>
<sup>1</sup>Jonas Schmedtmann. The Complete JavaScript Course 2020: Build Real Projects!. Retrieved June 06, 2020, from [https://www.udemy.com/course/the-complete-javascript-course/](https://www.udemy.com/course/the-complete-javascript-course/)<br/>