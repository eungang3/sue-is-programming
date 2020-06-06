---
layout: post
title:  "Javascript의 execution contexts와 execution stack"
date:   2020-06-06 01:40:27 +0900
categories: Javascript
---

Udemy - [The Complete JavaScript Course 2020: Build Real Projects!](https://www.udemy.com/course/the-complete-javascript-course/) 강좌의 섹션 3. How JavaScript Works Behind the Scenes와 Kyle Simpson의 책 [You don't know JS yet]((https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md))의 chapter 1 - get started를 요약한 내용입니다. 

<br/>


## Execution Context (실행 컨텍스트)
- js 코드를 실행하기 위해 필요한 환경
- 코드를 실행하는 상자같은 것이라고 생각하면 됨. 

### 1. Global Execution Context (GEC)
- 디폴트 환경, 단 하나만 존재함. 
- function 밖에 있는 모든 코드는 자동으로 global execution context로 실행.
- 

### 2. Function Execution Context(FEC)
- function body를 실행할 때 사용하는 환경

### 3. Eval Execution Context(EEC)
- internal eval function 속 코드 실행할 때 사용하는 환경 

<br/><br/>
출처 : <br/>
<sup>1</sup>Jonas Schmedtmann. The Complete JavaScript Course 2020: Build Real Projects!. Retrieved June 06, 2020, from [https://www.udemy.com/course/the-complete-javascript-course/](https://www.udemy.com/course/the-complete-javascript-course/)<br/>

<sup>2</sup>Simpson, K. (2019). You don't know JS yet: Get Started. Sebastopol, CA: O'Reilly Media. from [https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md)