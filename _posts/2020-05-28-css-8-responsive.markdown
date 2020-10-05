---
layout: post
title:  "CSS Responsive Web Design 구현하는 방법"
date:   2020-05-28 20:00:00 +0900
categories: CSS
---

## 0. Responsive Web Design이란?
- 한 웹사이트를 어떤 디바이스로 접근하더라도 괜찮아 보이게 디자인하는 방식.  

<br/>

## 1. CSS unit 적절하게 활용하기
### 1) Absolute Units(=fixed units)
- 절대적인 값 설정하는 unit(단위).
- 어떤 요소를 10px로 설정했으면 화면이 크건 작건 10px로 고정됨.
- 작은 화면에서 최소한의 크기를 유지해야하는 요소가 있을 때 드물게 사용.
- 예 : px, pt, pc, in, cm, mm

<br/>

### 2) Relative Units
#### a. Percentage Units
- 부모 요소를 기준으로 자식 요소의 상대적인 값 설정하는 unit.
- 주로 요소의 width 설정할 때 사용.

{% highlight css %}
.child-img {
   /* 자식을 px로 설정하면 부모 요소가 작아졌을 때 overflow 발생 가능 */
   /* %로 설정하면 부모가 작아져도 부모 width만큼만 차지 */
   /* BUT 부모가 자식 이미지 이상으로 커지면 화질 저하 발생 */
   width: 100%;
}
{% endhighlight %}

<br/>

#### cf) max-width / max-height
- 최대 너비/높이 설정.
- 어떤 요소의 너비/높이를 설정한 값 이상으로 커지지 않게 설정.

{% highlight css %}
.child-img {
   /* 부모가 아무리 커져도 원래 이미지 사이즈 이상으로 커지지 않음 */
   /* 자기 원래 너비의 100%까지만 커지겠다는 뜻 */
   max-width: 100%;
}
{% endhighlight %}

<br/>

#### cf) min-width / max-width
- 최소 너비/높이 설정.
- 어떤 요소의 너비/높이를 설정한 값 이상으로 작아지지 않게 설정.

{% highlight css %}
.child-img {
   /* 부모가 아무리 작아져도 20px보다 너비가 작아지지 않음 */
   min-width: 20px;
}
{% endhighlight %}

<br/>

#### b. Font relative units
- 폰트 크기를 기준으로 상대적인 값 설정하는 unit.
- Multi column layout의 width에는 사용 안하길 권장 (% 사용할 것)
- Multi column layout의 column-width에는 사용 가능 (% 사용 안됨)

* ex1) em
    - 해당 요소의 font-size값을 기준으로 삼음.
    - 해당 요소에 명시적으로 절대적 font-size값을 설정하지 않았다면 부모로 올라가면서 기준값을 찾음.
    - 해당 요소가 nested element일 때 예상치 못한 값 나올 수 있어서 곤란.
    - em 값의 기준이 되는 font-size는 rem으로 설정 권장. (상속 덜 헷갈림, 확장성 개선)
    - DO : 기본 font-size 값을 사용하지 않는 요소(=명시적으로 font-size를 기재한 요소)가 있는 부분에서, font-size 이외 프로퍼티 설정에 사용하기. (예 : 네비게이션 바의 padding, margin, line-height 값)
    - DON'T : font-size 프로퍼티에 사용하기 (BUT 드롭다운 메뉴의 글씨, 버튼 속 font icon 크기 설정엔 사용 OK)

{% highlight html %}
<head>
<style>
div {
  font-size : 8px;
}

p {
   /* 부모 div의 font-size의 2배, 즉 16px */
   font-size: 2em;
}

a {
   /* 부모 p의 font-size의 2배, 즉 32px */
   /* 같은 2em이지만 a가 더 커짐 */
   font-size: 2em;
}
</style>
</head>

<body>
   <div>
      <p>
       This is a paragraph.
        <a>This is anchor.</a>
      </p>
   </div>
</body>
{% endhighlight %}

<div style="font-size : 8px;"><p style="font-size: 2em;">This is a paragraph.<a style="font-size: 2em;">This is anchor.</a></p></div>

<br/>

- ex2) rem
    - Root Em의 줄임말.
    - root 요소(=html)의 font-size를 기준으로 삼음.
    - root 요소의 font-size값은 유저가 브라우저 설정에 등록한 값을 상속받음. (기본값 16px)
    - html 요소의 font-size 프로퍼티를 명시적으로 설정하면 브라우저 설정값 override 가능.
    - html 요소의 font-size 프로퍼티를 조절하고 싶다면 em이나 rem으로 할 것. px로 정해버리면 유저가 글씨 크거나 작게 보고 싶을 때 설정값 바꿔도 화면에 변화 없음 -> 사용자 경험 저해.
    - DO : 꼭 em을 사용해야 할 이유가 없다면 사용하기 (예 : height, width, padding, margin, font-size, shadows 등)
    - DON't : 브라우저 설정 font-size 값에 영향 받으면 안되는 곳에 사용하기

<br/>

#### c. Viewport relative units
- ex1) vh
    - viewport height의 줄임말.
    - 1vh는 viewport height의 1%

- ex2) vw
    - viewport width의 줄임말.
    - 1vh는 viewport width의 1%


## 2. Media Query 사용하기
- 특정 조건에서만 특정 CSS 반영되게 하는 방식. if문이라고 생각하면 됨. 
- 사용 방법 : @media media-type and (media-feature) { /* CSS rules */ }
- px, em, rem 모두 사용 가능한데 각각 장단점 있음. 
- cf) viewport: 유저에게 보이는 영역의 크기
- cf) breakpoint : 레이아웃 등의 변경이 일어나야 하는 지점의 값
- 논리 연산자(logical operator) 사용 가능
- ex1) and  
{% highlight css %}
/* media가 screen이고 viewport가 768px~1024px 사이의 값일 때 배경색 노랑 */
@media screen and (min-width: 768px) and (max-width: 1024px){
   background-color: yellow;
}
{% endhighlight %}

- ex2) or
 {% highlight css %}
/* media가 screen이고 viewport가 1024px 이상이거나 768px 이하일 때 배경색 노랑 */
@media screen and (min-width: 1024px), (max-width: 768px){
   background-color: yellow;
}
{% endhighlight %}

- ex3) not 
 {% highlight css %}
/* viewport가 768px가 아닐때만 배경색 노랑 */
/* not 사용할 때는 항상 media type 명시해야 함 */
@media not all and (width: 768px){
   background-color: yellow;
}
{% endhighlight %}

<br/>

### 1) media-type
- 브라우저에게 이것이 무슨 미디어를 위한 코드인지 말해줌
- {}안에 들어있는 CSS rule을 적용하기 위한 조건. 
- 생략하면 all(기본값)로 설정.
- 값 : all(기본값), print, screen, speech(스크린 리더 사용 시)
{% highlight css %}
/* media type이 screen이고 viewport가 500px일 때만 배경 노란색 적용 */
@media screen and (width: 500px) {
   body {
      background-color: yellow;
   }
}
{% endhighlight %}
{% highlight css %}
/* media type이 all이고 viewport가 500px일 때만 배경 노란색 적용 */
@media (width: 500px) {
   body {
      background-color: yellow;
   }
}
{% endhighlight %}
<br/>

### 2) media-feature
- {}안에 들어있는 CSS rule을 적용하기 위한 media의 상세한 조건. 

#### a. width / height로 설정
- width, height값으로 조건 설정. 
- 구체적인 breakpoint 값 지정하는 방식. 가장 자주 사용.
- 값 : min-width, max-width, width, height, max-height, max-width

{% highlight css %}
/* media type이 screen이고 viewport가 500px일 때만 배경 노란색 적용 */
@media screen and (width: 500px) {
   body {
      background-color: yellow;
   }
}
{% endhighlight %}

{% highlight css %}
/* media type이 screen이고 viewport가 768px 이하일 때만 배경 노란색 적용 */
@media screen and (max-width: 768px) {
   body {
      background-color: yellow;
   }
}
{% endhighlight %}

{% highlight css %}
/* media type이 screen이고 viewport가 768px 이상일 때만 배경 노란색 적용 */
@media screen and (min-width: 768px) {
   body {
      background-color: yellow;
   }
}
{% endhighlight %}

<br/>

#### b. orientation으로 설정
- 화면이 가로인지, 세로인지에 따른 조건 설정. 
- 값 : portrait(가로가 세로보다 짧을 때), landscape(가로가 세로보다 길 때)

{% highlight css %}
@media (orientation: landscape){
   div {
      flex-direction: row;
   }
}

@media (orientation: portrait){
   div {
      flex-direction: column;
   }
}
{% endhighlight %}

<br/>

#### c. pointing device 종류에 따라 설정
- pointing device에 따른 조건 설정. 
- 유저 인터랙션 고려한 디자인 구현 가능해짐. 
- hover 값 : hover, none
- pointer 값 : none(키보드나 voice commands 사용하는 디바이스), fine(마우스나 트랙패드 사용하는 디바이스), coarse(터치 사용하는 디바이스)
{% highlight css %}
/* hover 가능한 디바이스(마우스)에서만 배경색 노랑 */
@media (hover: hover){
   div {
      background-color: yellow;
   }
}
{% endhighlight %}

{% highlight css %}
/* 터치스크린 사용하는 디바이스에서만 배경색 노랑 */
@media (pointer: coarse){
   div {
      background-color: yellow;
   }
}
{% endhighlight %}

<br/>

### 3) CSS rules
- @media의 조건이 참일때 적용되는 코드.

<br/>

## 3. HTML 파일에 meta 요소 넣어서 viewport 설정하기
- head에 meta name="viewport" content="width=device-width, initial-scale=1.0"삽입.
- 현재 유저가 사용중인 스크린의 width를 viewport로 설정함. 
- 디폴트 설정에선 어떤 스크린에서 접근하든 width를 데스크탑 width로 자동 변환 -> 데스크탑 웹사이트를 모바일에서 보면 이미지, 글씨 작아짐. 

<br/><br/>
참조 :<br/>
[Free Code Camp - Responsive Web Design Principles](https://www.freecodecamp.org/learn)<br/>
[W3Schools.com - CSS Responsive](https://www.w3schools.com/css/css_rwd_intro.asp)<br/>
[Codecademy - Learn Responsive Design](https://www.codecademy.com/learn/learn-responsive-design)<br/>
[How to start thinking responsively](https://www.freecodecamp.org/news/how-to-start-thinking-responsively/)<br/>
[Comprehensive Guide : When to Use Em vs. Rem](https://webdesign.tutsplus.com/tutorials/comprehensive-guide-when-to-use-em-vs-rem--cms-23984?ec_unit=translation-info-language)<br/>
[MDN web docs - Beginner's guide to media queries](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Media_queries)<br/>
[Min-width, Max-width & Media Queries](https://medium.com/@banuriwickramarathna/min-width-max-width-media-queries-994e2ec5fca3)<br/>
[The 100% correct way to do CSS breakpoints](https://medium.com/free-code-camp/the-100-correct-way-to-do-css-breakpoints-88d6a5ba1862)
