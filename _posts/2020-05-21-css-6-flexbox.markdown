---
layout: post
title:  "CSS flexbox 이해하기"
date:   2020-05-21 21:00:00 +0900
categories: CSS
---

## 0. flexbox란?
- Flexible Box Layout. 유동적이고 responsive한 레이아웃을 쉽게 구현하기 위해 고안된 레이아웃 모델. 
- 부모-자식 필요 (ul과 li 태그처럼) : 부모의 display 값을 flex로 선언하면 부모는 flex container, 자식은 flex item이 됨.
- Flex container에 사용하는 프로퍼티 : display, flex-direction, flex-wrap, flex-flow, justify-content, align-content, align-items
- Flex item에 사용하는 프로퍼티 : order, flex-grow, flex-shrink, flex-basis, flex, align-self

<br/>

## 1. Flex container(부모)에 사용하는 프로퍼티
### 1) display
- flexbox 사용하기 위해 선언.
- 값: flex, inline-flex

{% highlight html %}
<head>
<style>
.parent {
    display: flex; /* 또는 inline-flex */
}
</style>
</head>

<body>
    <div class="parent"> <!-- flex container -->
        <div class="child"></div> <!-- flex item -->
    </div>
    <div class="parent"> <!-- flex container -->
        <div class="child"></div> <!-- flex item -->
    </div>
</body>
{% endhighlight %}

#### a. display: flex
- block 특성을 갖는 flexbox container를 만듦. (flex-item엔 영향 안미침)

<div style="display:flex;border:solid;"><div style="background-color: yellow">child1</div><div style="background-color: teal">child2</div><div style="background-color: green">child3</div></div><div style="display:flex;border:solid;"><div style="background-color: yellow">child1</div><div style="background-color: teal">child2</div><div style="background-color: green">child3</div></div>

<br/>

#### b. display: inline-flex
- inline 특성을 갖는 flexbox container를 만듦. (flex-item엔 영향 안미침)

<div style="display:inline-flex;border:solid;"><div style="background-color: yellow">child1</div><div style="background-color: teal">child2</div><div style="background-color: green">child3</div></div><div style="display:inline-flex;border:solid;"><div style="background-color: yellow">child1</div><div style="background-color: teal">child2</div><div style="background-color: green">child3</div></div>

<br/><br/>

### 2) flex-direction
- flex item의 주 축을 결정해줌. (=flex item을 어느 방향으로 쌓을 것인지 결정해줌) 
- 가로가 주축이면 가로로 쌓이고, 세로가 주축이면 세로로 쌓임. 
- 값: row(기본값, 가로가 주축), row-reverse, column, column-reverse

{% highlight html %}
<head>
<style>
.parent {
    display: flex;
    flex-direction: row; /* 또는 column 등 */
}
</style>
</head>

<body>
    <div class="parent"> <!-- flex container -->
        <div class="child1"></div> <!-- flex item -->
        <div class="child2"></div> <!-- flex item -->
        <div class="child3"></div> <!-- flex item -->
    </div>
</body>
{% endhighlight %}

#### a. flex-direction: row (가로 주축)
 <div style="display:flex;border:solid;"><div style="background-color: yellow">child1</div><div style="background-color: teal">child2</div><div style="background-color: green">child3</div></div>

<br/>

#### b. flex-direction: row-reverse
 <div style="display:flex;border:solid;flex-direction:row-reverse;"><div style="background-color: yellow">child1</div><div style="background-color: teal">child2</div><div style="background-color: green">child3</div></div>

<br/>

#### c. flex-direction: column (세로 주축)
 <div style="display:flex;border:solid;flex-direction:column;"><div style="background-color: yellow">child1</div><div style="background-color: teal">child2</div><div style="background-color: green">child3</div></div>

<br/>

#### d. flex-direction: column-reverse
 <div style="display:flex;border:solid;flex-direction:column-reverse;"><div style="background-color: yellow">child1</div><div style="background-color: teal">child2</div><div style="background-color: green">child3</div></div>

<br/><br/>

### 3) flex-wrap
- flex item이 여러 개 있고 브라우저 크기가 줄어들었을 때 줄바꿈 할 것인지 말 것인지 정함.
- 값: nowrap(기본값), wrap(줄바꿈), wrap-reverse(역방향으로 줄바꿈)

{% highlight html %}
<head>
<style>
.parent {
    display: flex;
    flex-wrap: wrap; /* 또는 wrap-reverse, nowrap */
}

.child {
    width: 150px; 
}

</style>
</head>

<body>
    <div class="parent"> <!-- flex container -->
        <div class="child1"></div> <!-- flex item -->
        <div class="child2"></div> <!-- flex item -->
        <div class="child3"></div> <!-- flex item -->
        <div class="child4"></div> <!-- flex item -->
    </div>
</body>
{% endhighlight %}

#### a. flex-wrap: nowrap
- 브라우저 크기를 줄이면 flex item의 width 설정 무시하고 줄여서 한 줄에 모두 넣음.  
<div style="display:flex;border:solid;"><div style="background-color: yellow;width:150px;">child1</div><div style="background-color: teal;width:150px;">child2</div><div style="background-color: green;width:150px;">child3</div><div style="background-color: blue;width:150px;">child4</div></div>

<br/>

#### b. flex-wrap: wrap
- 브라우저 크기 줄여도 flex item의 width 설정 유지. 한 줄에 안들어가면 부모 height 늘려서 줄바꿈. 
<div style="display:flex;border:solid;flex-wrap:wrap;"><div style="background-color: yellow;width:150px;">child1</div><div style="background-color: teal;width:150px;">child2</div><div style="background-color: green;width:150px;">child3</div><div style="background-color: blue;width:150px;">child4</div></div>

<br/>

#### c. flex-wrap: wrap-reverse
- wrap과 같은데 브라우저 크기 줄였을 때 역방향으로 배치. 
<div style="display:flex;border:solid;flex-wrap: wrap-reverse;"><div style="background-color: yellow;width:150px;">child1</div><div style="background-color: teal;width:150px;">child2</div><div style="background-color: green;width:150px;">child3</div><div style="background-color: blue;width:150px;">child4</div></div>

<br/>

### 4) flex-flow
- flex-direction 프로퍼티와 flex-wrap 프로퍼티를 동시에 설정하는 프로퍼티.
- 값: 'flex-direction 값(row, row-reverse, column, column-reverse 중 하나) 띄우고 flex-wrap 값(nowrap, wrap, wrap-reverse 중 하나)'으로 작성

{% highlight css %}
.parent{
    display: flex;
    flex-flow: column wrap; /* 세로방향으로 쌓고 줄바꿈하겠다는 뜻 */
}
{% endhighlight %}

<br/>

### 5) justify-content
- 주 축의 정렬 방법을 설정하는 프로퍼티. 
- 값: flex-start, flex-end, center, space-between, space-around

![flexbox1](https://eungang3.github.io/sue-is-programming/assets/flexbox1.jpg)
![flexbox2](https://eungang3.github.io/sue-is-programming/assets/flexbox2.jpg)
![flexbox3](https://eungang3.github.io/sue-is-programming/assets/flexbox3.jpg)
![flexbox4](https://eungang3.github.io/sue-is-programming/assets/flexbox4.jpg)

{% highlight html %}
<head>
<style>
.parent {
  display: flex;
  justify-content: flex-start; /* 주 축을 기준으로 정렬 */
  background-color: yellow;
}

.parent > div {
  background-color: white;
  width: 80px;
  margin: 5px;
}
</style>
</head>

<body>
<div class="parent">
  <div>1</div>
  <div>2</div>
  <div>3</div>  
</div>
</body>
{% endhighlight %}

#### a. justify-content: flex-start
- flex-item을 주 축의 flex-start에 붙임
- 주 축이 row인 경우:
<div style="display:flex;justify-content:flex-start;background-color:yellow;"><div style="background-color:white;width:80px;margin:5px;">1</div><div style="background-color:white;width:80px;margin:5px;">2</div><div style="background-color:white;width:80px;margin:5px;">3</div></div>

<br/>

#### b. justify-content: flex-end
- flex-item을 주 축의 flex-end에 붙임
- 주 축이 row인 경우:
<div style="display:flex;justify-content:flex-end;background-color:yellow;"><div style="background-color:white;width:80px;margin:5px;">1</div><div style="background-color:white;width:80px;margin:5px;">2</div><div style="background-color:white;width:80px;margin:5px;">3</div></div>

<br/>

#### c. justify-content: center
- flex-item을 주 축의 가운데를 기준으로 정렬
- 주 축이 row인 경우:
<div style="display:flex;justify-content:center;background-color:yellow;"><div style="background-color:white;width:80px;margin:5px;">1</div><div style="background-color:white;width:80px;margin:5px;">2</div><div style="background-color:white;width:80px;margin:5px;">3</div></div>

<br/>

#### d. justify-content: space-between
- 시작 item은 주 축의 flex-start에, 마지막 item은 주 축의 flex-end에 붙이고 나머지는 그 사이에 고르게 정렬
- 주 축이 row인 경우:
<div style="display:flex;justify-content:space-between;background-color:yellow;"><div style="background-color:white;width:80px;margin:5px;">1</div><div style="background-color:white;width:80px;margin:5px;">2</div><div style="background-color:white;width:80px;margin:5px;">3</div></div>

<br/>

#### e. justify-content: space-around
- flex-item을 주 축을 따라 균일하게 정렬
- 주 축이 row인 경우:
<div style="display:flex;justify-content:space-around;background-color:yellow;"><div style="background-color:white;width:80px;margin:5px;">1</div><div style="background-color:white;width:80px;margin:5px;">2</div><div style="background-color:white;width:80px;margin:5px;">3</div></div>

<br/>

### 6) align-content
- 교차 축의 정렬 방법을 설정하는 프로퍼티. 
- flex-wrap이 wrap으로 지정되어있고 item 줄바꿈이 최소 한 번은 일어나는 경우에만 적용됨. (한 줄만 있는 경우 align-items 프로퍼티 사용)
- flex container와 item들 간 여백이 없으면 효과 안보임.
- 값: stretch(기본값), flex-start, flex-end, center, space-between, space-around

{% highlight html %}
<head>
<style>
.parent {
  display: flex;
  background-color: yellow;
  height: 200px;
  flex-flow: row wrap;
  align-content: flex-end; /* flex-start 등 적용 */
}

.parent > div {
  background-color: white;
  width: 150px;
  margin: 5px;
}
</style>
</head>

<body>
<div class="parent">
  <div>1</div>
  <div>2</div>
  <div>3</div>  
  <div>4</div>
  <div>5</div>
  <div>6</div> 
</div>
</body>
{% endhighlight %}

#### a. align-content: stretch
- flex-item의 교차축 방향 값을 설정하지 않은 경우 교차축을 채우는 방향으로 늘어남. 
- 교차 축이 column인 경우:
<div style="display:flex;flex-flow:wrap;align-content: stretch;background-color:yellow;height:200px"><div style="background-color:white;width:150px;margin:5px;">1</div><div style="background-color:white;width:150px;margin:5px;">2</div><div style="background-color:white;width:150px;margin:5px;">3</div><div style="background-color:white;width:150px;margin:5px;">4</div><div style="background-color:white;width:150px;margin:5px;">5</div><div style="background-color:white;width:150px;margin:5px;">6</div></div>

<br/>

#### b. align-content: flex-start
- flex-item을 교차 축의 flex-start에 붙임
- 교차 축이 column인 경우:
<div style="display:flex;flex-flow:wrap;align-content:flex-start;background-color:yellow;height:200px"><div style="background-color:white;width:150px;margin:5px;">1</div><div style="background-color:white;width:150px;margin:5px;">2</div><div style="background-color:white;width:150px;margin:5px;">3</div><div style="background-color:white;width:150px;margin:5px;">4</div><div style="background-color:white;width:150px;margin:5px;">5</div><div style="background-color:white;width:150px;margin:5px;">6</div></div>

<br/>

#### c. align-content: flex-end
- flex-item을 교차 축의 flex-end에 붙임
- 교차 축이 column인 경우:
<div style="display:flex;flex-flow:wrap;align-content:flex-end;background-color:yellow;height:200px"><div style="background-color:white;width:150px;margin:5px;">1</div><div style="background-color:white;width:150px;margin:5px;">2</div><div style="background-color:white;width:150px;margin:5px;">3</div><div style="background-color:white;width:150px;margin:5px;">4</div><div style="background-color:white;width:150px;margin:5px;">5</div><div style="background-color:white;width:150px;margin:5px;">6</div></div>

<br/>

#### d. align-content: center
- flex-item을 교차 축의 가운데를 기준으로 정렬
- 교차 축이 column인 경우:
<div style="display:flex;flex-flow:wrap;align-content:center;background-color:yellow;height:200px"><div style="background-color:white;width:150px;margin:5px;">1</div><div style="background-color:white;width:150px;margin:5px;">2</div><div style="background-color:white;width:150px;margin:5px;">3</div><div style="background-color:white;width:150px;margin:5px;">4</div><div style="background-color:white;width:150px;margin:5px;">5</div><div style="background-color:white;width:150px;margin:5px;">6</div></div>

<br/>

#### e. align-content: space-between
- 시작 item은 교차 축의 flex-start에, 마지막 item은 교차 축의 flex-end에 붙이고 나머지 고르게 정렬
- 교차 축이 column인 경우:
<div style="display:flex;flex-flow:wrap;align-content:space-between;background-color:yellow;height:200px"><div style="background-color:white;width:150px;margin:5px;">1</div><div style="background-color:white;width:150px;margin:5px;">2</div><div style="background-color:white;width:150px;margin:5px;">3</div><div style="background-color:white;width:150px;margin:5px;">4</div><div style="background-color:white;width:150px;margin:5px;">5</div><div style="background-color:white;width:150px;margin:5px;">6</div></div>

<br/>

#### f. align-content: space-around
- flex-item을 교차 축을 따라 균일하게 정렬
- 교차 축이 column인 경우:
<div style="display:flex;flex-flow:wrap;align-content:space-around;background-color:yellow;height:200px"><div style="background-color:white;width:150px;margin:5px;">1</div><div style="background-color:white;width:150px;margin:5px;">2</div><div style="background-color:white;width:150px;margin:5px;">3</div><div style="background-color:white;width:150px;margin:5px;">4</div><div style="background-color:white;width:150px;margin:5px;">5</div><div style="background-color:white;width:150px;margin:5px;">6</div></div>

<br/>

### 7) align-items
- 교차 축에서 줄별로 정렬 방법을 설정하는 프로퍼티. 
- item이 한 줄일때 주로 사용
- flex-wrap이 wrap으로 지정되어있고 줄바꿈이 일어난 경우 align-content가 align-items를 이김 -> align-items 쓰려면 align-content 값을 기본값 stretch로 설정해야 함.  












<br/>

## 2. Flex item(자식)에 사용하는 프로퍼티






<br/><br/>

참조 :<br/>
[MDN web docs - flex](https://developer.mozilla.org/en-US/docs/Glossary/Flex)<br/>
[생활코딩 CSS 수업 - flex](https://opentutorials.org/course/2418/13526)<br/>
[Free Code Camp - CSS Flexbox](https://www.freecodecamp.org/learn)<br/>
[Naver D2 flexbox로 만들 수 있는 10가지 레이아웃](https://d2.naver.com/helloworld/8540176)<br/>
[W3Schools.com - CSS Flexbox](https://www.w3schools.com/css/css3_flexbox.asp)<br/>
[Heropy Tech - CSS Flex(Flexible Box) 완벽 가이드](https://heropy.blog/2018/11/24/css-flexible-box/)