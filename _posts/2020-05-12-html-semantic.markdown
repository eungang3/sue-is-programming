---
layout: post
title:  "웹 접근성을 높이는 방법"
date:   2020-05-13 21:35:27 +0900
categories: HTML
---

## 1. Semantic element 적재적소에 사용하기

### 0) Semantic element이란?
- __정의__ : 의미론적 요소. 감싸고 있는 부분이 페이지에서 어떤 역할을 하는지 알려주는 태그라는 뜻.  
- __사용 이유__ :
  + 검색엔진 최적화(SEO) : 검색 엔진이 내 웹페이지를 크롤링, 인덱싱하기 쉽게 해서 검색결과에 나오게 함. 
  + 장애인 유저 접근성 높임 : 스크린 리더로 웹페이지 브라우징하기 쉬워짐. 
  + 개발하기 편리 : 의미없는 div 사용하는 것 보다 검색, 수정 편리. 다른 개발자가 내 코드 이해하기도 편해짐. 

<br/>

### 1) Section heading (<h1> - <h6>)
- __의미__ : 여기에 section을 요약하는 타이틀이 있다. 
- __활용__ : 
  + 컨텐츠의 구조에 맞게 써야 함. 
  + h1 - h6까지 있음. h1이 가장 중요, 숫자 커질수록 중요도 떨어짐.
  + 숫자 건너뛰지 말고 써야 함. (h1 다음 h2도 없이 h3 쓰면 안됨). 
  + 한 웹페이지에는 무조건 하나의 h1태그가 있어야 하고 단 하나만 있어야 함. (검색엔진은 h1 태그안에 든 내용물 바탕으로 웹페이지 크롤링, 인덱싱)

{% highlight html %}
<h1>면의 종류</h1>  
  <h2>국수면</h2>  
    <h3>메밀국수면</h3>  
    <h3>쌀국수면</h3>  
  <h2>파스타면</h2>  
  <h2>우동면</h2>  
{% endhighlight %}

<br/>

### 2) header 
- __의미__ : 여기에 도입부가 있다.
- __활용__ : 
  + 전체 문서의 도입부에 사용 (로고, nav 등 nesting하기도 함)
  + 각 section의 도입부에 사용
  + h1 - h6 heading 태그 감싸는데 쓰려고 나왔지만 필수는 아님.
  + 한 페이지에 여러 번 사용 가능.
{% highlight html %}
<header>
<h1>면의 종류</h1>
<nav>
<ul>
  <li><a>국수면</a></li>
  <li><a>우동면</a></li>
</ul>
</nav>
</header>

<section>
  <header>
  <h2>국수면</h2>
  <p>국수면에 관해 알아보자.</p>
  </header>
  <p><!--국수면에 관한 내용--></p>
</section>
{% endhighlight %} 

<br/>

### 3) nav
- __의미__ : 여기에 네비게이션이 있다.
- __활용__ : 
  + 네비게이션 메뉴, 목차, 인덱스 등에 사용. 
  + 한 페이지에 여러 번 사용 가능.
  + 모든 링크에 사용할 필요는 없음. (예: 푸터에 들어간 링크 묶음엔 잘 안씀)

<br/>

### 4) main
- __의미__ : 여기에 메인이 있다.
- __활용__ : 
  + 한 페이지에 단 하나만 있어야 함.
  + 여러 웹페이지에서 반복되는 요소(로고, 검색창, 푸터, 링크 등)은 main에 넣으면 안됨.
  + article, aside, header, footer, nav 안에 main을 넣으면 안됨. 

<br/>

### 6) article
- __의미__ : 여기에 독립적인 컨텐츠 다발이 있다.
- __활용__ : 
  + 독립적으로 완결성 갖는 부분에 사용.
  + 웹페이지의 다른 요소를 다 제거해도 온전하게 존재할 수 있는 부분에 사용. 

<br/>

### 5) section
- __의미__ : 여기에 한 주제로 묶인 컨텐츠 다발이 있다.
- __활용__ : 
  + 주로 한 heading으로 묶인 영역에 사용. 
  + 한 페이지에 여러 번 사용 가능.

<br/>

### 7) aside
- __의미__ : 여기에 메인 컨텐츠와 간접적으로 연관된 정보가 있다. (가장 중요한 정보는 아니라는 뜻) 
- __활용__ : 
  + 메인 컨텐츠를 간접적으로 보조하는 정보에 사용. 

<br/>

### 8) footer
- __의미__ : 여기에 푸터가 있다.
- __활용__ : 
  + 섹션에 대한 정보 (작성자, 카피라이트, 링크 등) 표기할 때 사용

<br/>

### 9) figure, figcaption
- __의미__ : 여기에 시각자료가 있고, 이런 캡션이 달려있다.
- __활용__ : 시각적인 요소(이미지, 차트 등)를 <figure>로 감싸고 <figcaption>으로 캡션 제공하기
- __사용 이유__ : 연관된 요소를 묶고 대안이 되는 텍스트를 제시함으로써 접근성을 두 배 높임

{% highlight html %}
<figure>  
<img src="foo.jpeg" alt="Picture of a cat drinking milk">  
<figcaption>  
A cat is drinking milk.  
</figcaption>  
</figure>
{% endhighlight %}

<br/>

### 10) fieldset
- __의미__ : 여기에 fieldset이 있고, 이 fieldset의 목적은 <legend>을 보면 알 수 있다.
- __활용__ : fieldset 태그로 라디오 버튼 모두 감싸고 legend 태그로 fieldset 설명 감싸기

{% highlight html %}
<form>
<fieldset>
<legend>하나를 고르세요</legend>
<label for="one">첫번째</label>
<input id="one" type="radio" name="items" value="first">
<label for="two">두번째</label>
<input id="two" type="radio" name="items" value="second">
</fieldset>
</form>
{% endhighlight %}

<br/>

## 2. tag 속성 값 알맞게 지정하기
### 1) img태그에 alt 속성 부여하기
- __활용__ :  
  + 해당 이미지를 설명하는 간단한 글 입력. "이미지가 없을 때 이 글을 띄워줘"라는 의미.    
  + HTML5부터는 의무적으로 작성해야 함. 작성하지 않을 시 장애인 차별금지법에 근거한 법적인 문제가 생길 수 있음.
- __사용 이유__ :  
  + 이미지를 로드할 수 없을 때 브라우저가 대신 화면에 나타낼 수 있는 정보를 제시함.  
  + 시각장애인이 사용하는 스크린 리더가 이미지에 대한 정보도 읽을 수 있게 함.  
  + 검색 엔진이 수집할 수 있는 정보 제공.  
- __예외__ : 순수하게 장식적인 이미지라면 alt에 아무것도 넣지 않아도 됨. 

{% highlight html %}
<img src="foo.jpeg" alt="">
{% endhighlight %}

{% highlight html %}
<img src="foo.jpeg" alt="Picture of a cat">
{% endhighlight %}

<br/>

### 2) audio 태그 사용 시 캡션이나 설명, 링크 제공하기

{% highlight html %}
<audio id="foo" controls>
<source src="audio/bar.mp3" type="audio/mpeg"/>
</audio>
{% endhighlight %}

<br/>

### 3) label 태그에 for 속성 제공하기
- __활용__ : form control의 id와 같은 값 입력
- __사용 이유__ : 
  + 어떤 텍스트가 어떤 form control과 연관되는지 스크린 리더가 읽을 수 있게 함, 
  + form control이 작을 때(예: 라디오 버튼)클릭하기 어려운데, label 영역 지정하면 label 클릭해서 form control 조작 가능함.  

{% highlight html %}
<form>
<label for="name">이름</label>
<input type="text" id="name" name="name">
</form>
{% endhighlight %}   

<br/>

### 4) time 태그에 datetime 속성 부여하기
- __활용__ : time 태그의 datetime 속성에 표준시 입력

{% highlight html %}
다음 모임은 <time datetime="2020-05-12">5월 12일</time>에 있을 예정입니다.
{% endhighlight %}

<br/><br/>
참조 : <br/>
[Free Code Camp의 Applied Accessibility 항목](https://www.freecodecamp.org/learn)<br/> 
[https://poiemaweb.com/html5-semantic-web](https://poiemaweb.com/html5-semantic-web)<br/>
[MDN web docs - Semantics](https://developer.mozilla.org/en-US/docs/Glossary/Semantics)<br/>
[W3Schools.com - HTML Sematic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)<br/>
[A Look Into Proper HTML5 Semantics](https://www.hongkiat.com/blog/html-5-semantics/)

