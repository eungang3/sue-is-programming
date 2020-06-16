---
layout: post
title:  "Javascript 문장 VS 표현식"
date:   2020-06-16 01:40:27 +0900
categories: Javascript
---

## 0. 문장 (Statements)
- 동작을 실행하는 코드

- 표현식, 연산자(예: +), 키워드(예: if, var) 등으로 구성됨.

- 예 :
    + function declarations
    + if statement
    + switch statement
    + a = b + 2;

<br/>
- 값을 내놓는 문장은 expression statement라고 함

- 예 :
    + 3+5;
    + functionCall();

<br/>
- 세미콜론 연산자 이용하여 묶을 있음
{% highlight javascript %}
function test(); var x; const y = 10;
{% endhighlight %}

<br/>

### cf) Block statements
- {} : 하나 이상의 expression statements나 statements를 묶어서 block statements로 만드는 역할.

- label : expression, statements, expression statements 앞에 붙여서 지칭하는 역할 (variable 아님, 필수적인 것 아님). 

{% highlight javascript %}
// loop:이 label
loop: {
    for (const i = 0; i < 10; i++){
        for (const j = 0; j < 10; j++>){
            break loop // 두 loop 모두 깨짐 
        }
    }
}
{% endhighlight %}

{% highlight javascript %}
{const x = 2, test(), 3} //3 출력
console.log(x); //2 출력
console.log({const x = 2, test(), 3}); // 에러 
// statement이기 때문에 console.log의 인자로 넣을 수 없음
{% endhighlight %}

{% highlight javascript %}
{2+3} + 3 // 3 출력
// statement이기 때문에 값을 내놓지 않음 -> 
// +를 보고 {}를 스트링이나 숫자로 자동 변환 시도 ->
// 불가능하기 때문에 {}에서 0 리턴  
{% endhighlight %}
<br/>

## 1. 표현식 (Expressions)
- 값을 내놓는 코드.

- 예 :
    + function expressions
    + literal values(예: 2)
    + 3 + 5
    + functionCall()
    + isSleepy ? sleep() : study()

<br/>
- cf) literals : 코드에 바로 사용할 수 있는 고정된 값 (예: array literals, numeric literals...)

- 표현식인 function call에 상태 변경하는 문장을 넣을 경우 :
{% highlight javascript %}
// 권장하지 않음
const foo = function(){
   exampleVariable = 1;
}
{% endhighlight %}

{% highlight javascript %}
// 권장 방식.
// 표현식과 문장을 분리해서 가독성 높이고 유지보수 쉬워짐.  
const foo = function(n){
   return n;
}
exampleVariable = foo(1);
{% endhighlight %}

<br/>
- 괄호와 콜론 연산자 이용하여 묶을 수 있음 
    + 왼쪽->오른쪽으로 parsing해서 제일 오른쪽에 있는 것만 리턴
    + js 엔진은 괄호를 보면 표현식으로 인식 -> 값을 내놓기를 바람. 
{% highlight javascript %}
console.log((5, function (){}, a)) // a만 출력
console.log(5, function (){}, a) // 4개 다 출력
{% endhighlight %}

<br/><br/>
출처 : <br/>
<sup>1</sup>Tochi, P. (2017, October 21). All you need to know about Javascript's Expressions, Statements and Expression Statements. Retrieved June 16, 2020, from [https://dev.to/promhize/javascript-in-depth-all-you-need-to-know-about-expressions-statements-and-expression-statements-5k2](https://dev.to/promhize/javascript-in-depth-all-you-need-to-know-about-expressions-statements-and-expression-statements-5k2)<br/>
<sup>2</sup>Simpson, K. (2015, July 01). You don't know JS: Up &amp; going. Retrieved June 16, 2020, from [https://www.oreilly.com/content/you-dont-know-js-up-going/](https://www.oreilly.com/content/you-dont-know-js-up-going/)<br/>
<sup>3</sup>(n.d.). Retrieved June 16, 2020, from [https://2ality.com/2012/09/expressions-vs-statements.html](https://2ality.com/2012/09/expressions-vs-statements.html)





https://github.com/leonardomso/33-js-concepts#7-expression-vs-statement