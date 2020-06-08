---
layout: post
title:  "Javascript의 실행 과정"
date:   2020-06-06 01:35:27 +0900
categories: Javascript
---

Udemy - [The Complete JavaScript Course 2020: Build Real Projects!](https://www.udemy.com/course/the-complete-javascript-course/) 강좌의 섹션 3. How JavaScript Works Behind the Scenes와 Kyle Simpson의 책 [You don't know JS yet:get started]((https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md)), [You don't know JS yet: Scope & Closuers](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md)를 요약한 내용입니다. 

<br/>


## Interpreted languages VS Compiled languages
- js는 흔히들 interpreted language(=scripting language)라고 하지만 근본적으론 compiled language.
- js가 왜 compiled language에 가까운 지 알아야 스코프를 이해할 수 있음.

### 1) Interpreted languages의 실행 과정
![js-how1](https://eungang3.github.io/sue-is-programming/assets/js-how1.jpg)
1. 한줄씩 실행 
2. 5번째 줄에 에러가 있으면 1~4번째줄까지 실행한 다음 에러 발생.
3. static error(=syntax error)도 실행 중에 알려줌.

<br/>

### 2) Compiled languages의 실행 과정
![js-how2](https://eungang3.github.io/sue-is-programming/assets/js-how2.jpg)
1. 전체 코드를 processing(주로 parsing을 뜻함)한 다음 실행. 
2. 5번째 줄에 에러가 있으면 실행 전 parsing 단계에서 에러 발생 -> 프로그램 전체가 실행 안됨.
3. static error가 있으면 실행 전 parsing 단계에서 알려줌. 
4. parsing 완료 후, parsing된 코드를 compile해서 실행가능한 형태의 machine code 생성
- 보통 compiled languages는 여기서 machine code를 만들어놓고 배포할 때 쓰는데, js는 machine code는 만들어놓고 배포할 때는 source code를 써서 js는 compiled language가 아니라는 잘못된 주장이 나옴. 
5. compile된 코드 실행

<br/>

#### cf) Compile의 세 단계
1. Tokenizing/lexing : 코드를 의미있는 단위(token)로 나누는 과정. 
- ex : var example = 1;은 다섯가지 토큰으로 나뉨(var, example, =, 1, ;)

2. Parsing : token을 모아 AST로 만드는 과정. 
![js-how4](https://eungang3.github.io/sue-is-programming/assets/js-how4.jpg)

3. Code generation : AST를 컴퓨터가 읽고 실행 가능한 코드로 바꾸는 과정. 언어마다 자세한 사항은 다름. 

<br/>

### 3) js의 실행 과정
![js-how3](https://eungang3.github.io/sue-is-programming/assets/js-how3.jpg)
1. 코드 작성
2. babel로 해당 코드 transpile
3. transpiled된 코드에 webpack으로 필요한 build 같이 꾸려줌.
4. 브라우저의 JS engine(js 코드 실행해주는 프로그램. ex: chrome의 v8)에 도착
5. JS engine으로 코드 Tokenizing/lexing.
6. JS engine으로 코드 parsing -> __static error가 있으면 이 단계에서 오류 내고 진행 중단__ -> 문제 없으면 AST 생성
7. JS engine으로 AST를 기계가 이해할 수 있는 코드인 binary IR(Intermediate Representation)로 변환
8. JIT compiler로 binary IR 최적화된 상태로 변환
9. JS VM(=JS Virtual Machine)으로 실행 

<br/>

## 결론
- js는 코드를 parsing/compilation한 다음에 실행한다.
- 이에 따른 js의 행동: 
    + 뒷줄에 있는 function에 오류가 나면 앞 줄에 있는 코드는 아예 실행 안됨
    + Hoisting (function, variable을 컴파일 단계에서 메모리에 저장해서, 코드 실행 전에 사용 가능한 상태로 만들어주는 것.) 
 
{% highlight javascript %}
var greeting = "hey"; 

cosole.log(greeting); //프린트 안됨 
//(컴파일 단계에서 SyntaxError 발생했기 때문에 실행단계까지 안 감)

greeting = ."Hi"; //SyntaxError: unexpected token .
{% endhighlight %}

{% highlight javascript %}


console.log("Hello");
//프린트 안됨 (컴파일 단계에서 SyntaxError 발생했기 때문에 실행단계까지 안 감)

greet("Hey", "Hi");
//Uncaught SyntaxError: Duplicate parameter name
//not allowed in this context 

function greet(greeting, greeting){
    "use strict"; //이 모드에서는 동일한 파라미터 이름 금지됨.
    console.log(greeting);
}
{% endhighlight %}


<br/><br/>
출처 : <br/>
<sup>1</sup>Jonas Schmedtmann. The Complete JavaScript Course 2020: Build Real Projects!. Retrieved June 06, 2020, from [https://www.udemy.com/course/the-complete-javascript-course/](https://www.udemy.com/course/the-complete-javascript-course/)<br/>

<sup>2</sup>Simpson, K. (2019). You don't know JS yet: Get Started. Sebastopol, CA: O'Reilly Media. from [https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md)