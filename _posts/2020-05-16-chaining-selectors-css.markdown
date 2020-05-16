---
layout: post
title:  "CSS 선택자 올바르게 사용하기"
date:   2020-05-12 21:35:27 +0900
categories: HTML
---

## 0. 선택자란?
스타일을 입힐 요소를 선택하게 해주는 것.  

<br/>

## 1. 단순 선택자 (simple selectors)
### 1) 전체 선택자 (universal selector)
페이지의 모든 요소를 선택. 자식 요소까지 선택할 수 있음. * 써서 사용.

{% highlight css %}
/* padding, margin, border를 0으로 초기화 */
/* 브라우저마다 다른 디폴트 값 초기화하기 위해 쓰는 방법 */

* {
    padding: 0;
    margin: 0;
    border: 0;
}
{% endhighlight %}

<br/>

### 2) 타입 선택자 (type selector)
html 요소를 선택. 요소 이름(ex. p) 써서 사용. 선택한 요소의 하위 요소 모두 상속 적용됨. (BUT 패딩, 보더 같은 배치 관련 속성은 상속 안됨.)

{% highlight html %}
<!-- 페이지 내 div과 div의 자식까지 전부 중앙 정렬함. -->
<head>
<style>
div {
  text-align: center;
}
</style>
</head>

<body>
    <div>
        <p>div의 첫번째 자식 p</p>
        <p>div 두번째 자식 p</p>
        <section>
            <p>div의 세번째 자식 section의 자식 p</p>
        </section>
    </div>
    <p>div 자식 아님</p>

</body>
{% endhighlight %}

<pre><div style="text-align: center;"><p>div의 첫번째 자식 p</p><p>div 두번째 자식 p</p><section><p>div의 세번째 자식 section의 자식 p</p></section></div><p>div 자식 아님</p></pre>

<br/>

### 3) 클래스 선택자 (class selector)
특정 클래스 갖는 요소 선택. 클래스 이름 앞에 '.' 붙여서 사용. 문서 내 여러 개 요소에 중복 사용 가능.

{% highlight css %}
/* contact class 갖는 모든 요소의 배경색을 파랑으로 지정 */

.contact {
    background-color: blue;
}
{% endhighlight %}


<br/>

### 4) 아이디 선택자 (id selector)
특정 아이디 갖는 요소 선택. 클래스 이름 앞에 '#' 붙여서 사용. 문서 당 __하나만__ 사용 가능. 특별한 제어, 검색이 쉬워짐.

{% highlight css %}
/* summary 아이디를 가진 유일한 요소의 배경색을 파랑으로 지정 */

#summary {
    background-color: blue;
}
{% endhighlight %}

<br/>

### 5) 그룹 선택자 (group selector)
여러 요소를 ','로 연결해서 동시에 선택. 쉼표로 연결된 요소는 서로 아무 상관 없음. 같은 스타일이 들어가는 여러 개의 요소를 각각 쓰면 너무 길어지니까 동시에 부르는 방법.

{% highlight css %}
/* 모든 div, p, summary 클래스의 텍스트를 중앙정렬 */

div, p, .summary {
    text-align: center;
}
{% endhighlight %}

<br/><br/>

## 2. 복합 선택자 (combinator selectors)

서로 연관된 단순 선택자들을 연결자(combinator)로 연결해서 만드는 선택자.

<br/>

### 1) 하위 선택자 (descendant selector)
- 자손 요소(자식, 자식의 자식 이하 모두 포함)를 선택. 두 개 이상의 선택자를 공백으로 분리해서 사용. 
{% highlight html %}
<!--div의 자손 중 p만 배경색을 노랑으로 지정. -->

<head>
<style>
div p {
  background-color: yellow;
}
</style>
</head>

<body>
    <div>
    <p>div의 첫번째 자식 p</p>
    <p>div 두번째 자식 p</p>
    <section>
        <p>div의 세번째 자식 section의 첫번쨰 자식 p</p>
        <a>div의 세번째 자식 section의 두번째 자식 a</a>
    </section>
    <a href="#">div의 네번째 자식 a</a>
    </div>
    <p>div 자식 아님</p>
</body>
{% endhighlight %}

<pre><div><p style="background-color: yellow">div의 첫번째 자식 p</p><p style="background-color: yellow">div의 두번째 자식 p</p><section><p style="background-color: yellow">div의 세번째 자식 section의 첫번째 자식 p</p><a>div의 세번째 자식 section의 두번째 자식 a</a></section><a href="#">div의 네번째 자식 a</a></div><p>div 자식 아님</p></pre>

<br/>

### 2) 자식 선택자 (child selector)
자식 요소(한 단계 아래에 있는 직계 자식만 해당. 자식의 자식은 해당 안됨)를 선택. 두 개 이상의 선택자를 '>'로 분리해서 사용. 

{% highlight html %}
<!--div의 자식 중 p만 배경색을 노랑으로 지정. -->

<head>
<style>
div > p {
  background-color: yellow;
}
</style>
</head>

<body>
    <div>
    <p>div의 첫번째 자식 p</p>
    <p>div 두번째 자식 p</p>
    <section><p>div의 세번째 자식 section의 자식 p</p></section>
    <a href="#">div의 네번째 자식 a</a>
    </div>
    <p>div 자식 아님</p>
</body>
{% endhighlight %}

<pre><div><p style="background-color: yellow">div의 첫번째 자식 p</p><p style="background-color: yellow">div의 두번째 자식 p</p><section><p>div의 세번째 자식 section의 첫번째 자식 p</p><a>div의 세번째 자식 section의 두번째 자식 a</a></section><a href="#">div의 네번째 자식 a</a></div><p>div 자식 아님</p></pre>

<br/>

### 3) 인접 형제 선택자 (sibling selector)
어떤 요소의 첫째 동생만 선택. 두 개 이상의 선택자를 '+'로 분리해서 사용. 

{% highlight html %}
<!--div의 형제 p 중 첫째 동생인 것만 배경색을 노랑으로 지정. -->
<head>
<style>
div + p {
  background-color: yellow;
}
</style>
</head>

<body>
    <p>div의 형</p>
    <div>
        <p>div의 자식 p</p>
    </div>
    <p>div의 첫째 동생 p</p>
    <p>div의 둘째 동생 p</p>
</body>
{% endhighlight %}

<pre><p>div의 형</p><div><p>div의 자식 p</p></div><p style="background-color: yellow">div의 첫째 동생 p</p><p>div의 둘째 동생 p</p></pre>

<br/>

### 4) 일반 형제 선택자 (sibling selector)
어떤 요소의 모든 동생을 선택. 두 개 이상의 선택자를 '~'로 분리해서 사용. 

{% highlight html %}
<!--div의 형제 p 중 모든 동생의 배경색을 노랑으로 지정. -->
<head>
<style>
div ~ p {
  background-color: yellow;
}
</style>
</head>

<body>
    <p>div의 형</p>
    <div>
        <p>div의 자식 p</p>
    </div>
    <p>div의 첫째 동생 p</p>
    <p>div의 둘째 동생 p</p>
</body>
{% endhighlight %}

<pre><p>div의 형</p><div><p>div의 자식 p</p></div><p style="background-color: yellow">div의 첫째 동생 p</p><p style="background-color: yellow">div의 둘째 동생 p</p></pre>

<br/>

## 3. 속성 선택자 (attribute selectors)
속성으로 요소를 선택할 수 있게 해주는 선택자.

### 1) [attribute] selector
특정 속성을 갖고 있는 것은 모두 선택

{% highlight css %}
/* alt 속성을 갖고 있는 모든 img 가로를 100px으로 설정 */

img[alt]{
    width: 100px;
}
{% endhighlight %}

<br/>

### 2) [attribute="value"] selector
특정 속성을 갖고 있고 특정한 속성값을 갖는 것만 선택

{% highlight css %}
/* target 속성이 "_blank"인 모든 a를 가운데 정렬 */

a[target="_blank"]{
    text-align: center;
}
{% endhighlight %}

<br/>

### 3) [attribute~="value"] selector
속성값에 특정 단어가 들어간 것을 모두 선택

{% highlight css %}
/* class 속성값 "top"이 들어간 모든 요소를 가운데 정렬 */
/* "top text"나 "top", "text top"은 선택하지만 "toptext"나 "top-text"는 선택 못함 */

[class~="top"]{
    text-align: center;
}
{% endhighlight %}

<br/>

### 4) [attribute|=value] selector
속성값이 특정 단어로 시작하는 것을 모두 선택. IE8이하에서 쓰려면 DOCTYPE 선언 필수

{% highlight css %}
/* class 속성값이 "top"으로 시작하는 모든 요소를 가운데 정렬 */
/* "top-text"나 "top"은 선택하지만 "toptext"는 선택 못함 */

[class|="top"]{
    text-align: center;
}
{% endhighlight %}

<br/>

### 5) [attribute^="value"] selector
속성값이 특정 문자열로 시작하는 것을 모두 선택. IE8이하에서 쓰려면 DOCTYPE 선언 필수

{% highlight css %}
/* class 속성값에 "top"이 들어가는 모든 요소를 가운데 정렬 */
/* "top-text", "top", "toptext", "top text" 모두 선택 가능 */

[class^="top"]{
    text-align: center;
}
{% endhighlight %}

<br/>

### 6) [attribute$="value"] selector
속성값이 특정 문자열로 끝나는 것을 모두 선택. 

{% highlight css %}
/* class 속성값에 "top"이 들어가는 모든 요소를 가운데 정렬 */
/* "text-top", "top", "texttop", "text top" 모두 선택 가능 */

[class$="top"]{
    text-align: center;
}
{% endhighlight %}

<br/>

### 7) [attribute*="value"] selector
속성값이 특정 문자열이 들어있는 것을 모두 선택.

{% highlight css %}
/* class 속성값에 "top"이 들어가는 모든 요소를 가운데 정렬 */
/* "talon", "table", "tarrot", "table top" 모두 선택 가능 */

[class*="top"]{
    text-align: center;
}
{% endhighlight %}

<br/>

## 4. 가상 클래스(pseudo-class)
가상 클래스는 요소나 속성이 아닌 상황을 선택할 수 있게 해줌.

### 1) :first-child
어떤 요소가 첫번째 자식이면서 :앞에 입력한 요소와 같은 상황일 때 선택함.

{% highlight html %}
<!-- 문서 내 모든 요소 중 첫번째 자식이면서 p인 것을 선택 -->

<style>
p:first-child {
  background-color: yellow;
}
</style>
</head>

<body>
<p>body의 첫번째 자식 p</p> <!-- 선택 -->
<h1>body의 두번째 자식 h1</h1>
<div>
  <p>div의 첫번째 자식 p</p> <!-- 선택 -->
  <p>div의 두번째 자식 p</p>
</div>
<p>body의 세번째 자식 p</p>
</body>
{% endhighlight %}

<pre><p style="background-color: yellow">body의 첫번째 자식 p</p><h1>body의 두번째 자식 h1</h1><div><p style="background-color: yellow">div의 첫번째 자식 p</p><p>div의 두번째 자식 p</p></div><p>body의 세번째 자식</p></pre>

<br/>

### 2) :nth-child()
어떤 요소가 괄호에 입력한 숫자번째 자식이고 :앞에 입력한 요소와 같은 상황일 때 선택함. 

{% highlight html %}
<!-- 문서 내 모든 요소 중 두번째 자식이면서 p인 것을 선택 -->

<style>
p:nth-child(2) {
  background-color: yellow;
}
</style>
</head>

<body>
<p>body의 첫번째 자식 p</p>
<h1>body의 두번째 자식 h1</h1>
<div>
  <p>div의 첫번째 자식 p</p>
  <p>div의 두번째 자식 p</p> <!-- 선택 -->
</div>
<p>body의 세번째 자식</p>
</body>
{% endhighlight %}

<pre><p>body의 첫번째 자식 p</p><h1>body의 두번째 자식 h1</h1><div><p>div의 첫번째 자식 p</p><p style="background-color: yellow">div의 두번째 자식 p</p></div><p>body의 세번째 자식</p></pre>

<br/>

### 3) :link, :visited, :hover
링크 방문 전인 상황, 방문 후의 상황, 마우스를 올려놓는 중인 상황일 때 각각 선택함. 

{% highlight html %}
<!-- 방문한 적 없는 링크 -->
a:link{
    color: yellow;
}

<!-- 방문한 적 있는 링크 -->
a:visited{
    color: blue;
}

<!-- 링크에 마우스 올렸을 때 -->
a:hover{
    color: red;
}

{% endhighlight %}

<br/>

### 4) :active
마우스를 눌렀다 놓는 동안일 때 선택.

{% highlight html %}
<!-- 마우스 눌렀다 놓는동안 글자색 노랑으로 변경 -->

a:active{
    color: yellow;
}
{% endhighlight %}

<br/>

### 5) :focus
텍스트 입력 폼 클릭하고 입력하는 상황일 때 선택.

{% highlight html %}
<!-- 텍스트 인풋필드 클릭하면 노랑으로 변경 -->

input:focus{
    background-color: yellow;
}
{% endhighlight %}

<br/>

### 6) :lang()
()에 입력한 언어가 사용된 상황일 때 선택. 

{% highlight html %}
<!-- 문서 내 영어는 배경을 노랑으로 변경 -->
<head>
<style>
    html:lang(eng){
        background: yellow;
    }
</style>

<body>
<p lang="eng">Yay</p>
</body>

{% endhighlight %}

<br/>

## 5. 가상 요소(pseudo-element)
XHTML(EXtensible HTML. HTML과 비슷하지만 문법이 더 엄격)에서 최초의 줄이나 문자 등 지정할 수 있게 해줌. CSS3부터 ::로 사용.
IE 5.5 - 8에선 CSS2 문법인 :로 사용해야 작동함. 

### 1) ::first-line
- 문단 첫번째 줄 선택.
- block level 요소에만 적용됨.
- font와 color 속성, background, word-spacing, letter-spacing, text-decoration, vertical-align, text-transform, line-height, text-shadow, clear만 적용 가능.

{% highlight html %}
<!-- 문서 내 모든 p의 첫줄 선택 -->

p::first-line {      
    line-height: 10px;
}
{% endhighlight %}

<br/>

### 2) ::first-letter
- 요소의 첫번째 글자 선택. 첫번째 글자 앞에 인용부호나 괄호가 있으면 그것 포함 첫번째 글자. 
- block level 요소에만 적용됨.
- first-line과 충돌 일어나면 first-letter가 이김
- font와 color 속성, background, margin, padding, border, text-decoration, vertical-align(float이 none일때만), text-transform, line-height, float, text-shadow, clear만 적용 가능. 

{% highlight html %}
<!-- 문서 내 모든 p의 첫번째 글자 선택 -->

p::first-letter {  
    text-transform: uppercase;
}
{% endhighlight %}

<br/>

### 3) ::before, ::after
요소의 앞과 뒤에 삽입할 때 사용.

{% highlight html %}
<!-- 문서 내 모든 p 앞에 '주의' 삽입 -->
p::before {
    content: "주의 - "
}

<!-- 문서 내 모든 p 뒤에 '!' 삽입 -->
p::after {
    content: "!"
}
{% endhighlight %}


<br/><br/>

참조 : [생활코딩 CSS Reference](https://www.opentutorials.org/module/484/4150),
[w3schools.com](https://www.w3schools.com/cssref/css_selectors.asp), 
[edwith 초보자를 위한 HTML & CSS 동작과 원리](https://www.edwith.org/htmlcss/joinLectures/12826?null)
