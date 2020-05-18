---
layout: post
title:  "CSS 박스 모델 이해하기"
date:   2020-05-12 21:35:27 +0900
categories: HTML
---

## 0. 박스 모델이란?
- 모든 html 요소는 박스 모델을 따름. (=모든 html 요소는 박스 안에 들어가 있음). 
- property : width, height, border, padding, margin

![box1](https://eungang3.github.io/sue-is-programming/assets/box1.jpg)

<br/>

## 1. 박스 property

### 1) Border
- Content를 감싸는 라인. 
- style, width, color 지정할 수 있음.

{% highlight css %}
/* content인 h1이 살고있는 박스의 border 값 변경 */

h1 {  
    border: 3px solid blue; /* 순서 상관 없음 */
    border-radius: 4px; /* 모서리 라운드 처리, 값 100%는 원 */
}
{% endhighlight %}

<br/>

### 2) Padding
- Content와 border 사이의 공간

{% highlight css %}
/* 1. 값 각각 지정하기 */

h1 {  
    padding-top: 10px;
    padding-right: 20px;
    padding-bottom: 30px;
    padding-left: 40px; 
}

/* 2. 한 번에 지정하기(시계방향으로 상, 우, 하, 좌) */

h2 {  
    padding: 10px 20px 30px 40px; 
}

/* 3. 한 번에 지정하기(상하, 좌우) */

h3 {  
    padding: 20px 40px; 
}

/* 4. 한 번에 지정하기(상하좌우) */

h4 {  
    padding: 20px; 
}
{% endhighlight %}

<br/>

### 3) Margin
- border 바깥 공간

{% highlight css %}
/* 1. 값 각각 지정하기 */

h1 {  
    margin-top: 10px;
    margin-right: 20px;
    margin-bottom: 30px;
    margin-left: 40px; 
}

/* 2. 한 번에 지정하기(시계방향으로 상, 우, 하, 좌) */

h2 {  
    margin: 10px 20px 30px 40px; 
}

/* 3. 한 번에 지정하기(상하, 좌우) */

h3 {  
    margin: 20px 40px; 
}

/* 4. 한 번에 지정하기(상하좌우) */

h4 {  
    margin: 20px; 
}
{% endhighlight %}

<br/>

#### a. margin auto
auto값 지정하면 부모 박스 가로축으로 가운데 정렬 가능. 단, 블록 레벨 요소인 div 등은 디폴트 width가 전체 화면을 채우게 되어있으므로 width값을 따로 설정해줘야 효과를 볼 수 있음.

{% highlight html %}
<!-- 부모인 div container 속 자식 div 가운데 정렬하기 -->

<div style="border: 1px solid">
  <div style="background-color: yellow; width: 300px; margin: auto; 
  text-align: center;">
  자식 div
  </div>
</div>

{% endhighlight %}

<pre><div class="parent" style="border: 1px solid"><div class="child" style="background-color: yellow; width: 300px; margin: auto; text-align: center;">자식의 margin이 auto일 때</div></div></pre>

<pre><div class="parent" style="border: 1px solid"><div class="child" style="background-color: yellow; width: 300px;text-align: center;">자식의 margin 설정 없을 때</div></div></pre>

<pre><div class="parent" style="border: 1px solid"><div class="child" style="background-color: yellow; text-align: center;">자식의 width 설정 없을 때</div></div></pre>

<br/>

#### b. margin collapse
상하로 박스 두개가 만나면, 더 큰 마진만 적용됨. (BUT 인라인 요소의 박스인 경우 상하로 만나더라도 마진의 합으로 적용)

![box2](/assets/box2.jpg)

<br/>

![box3](/assets/box3.jpg)

<br/>

## 4) min/max width/height
- 작거나 큰 디바이스에서 접근했을 때 박스가 너무 작아지거나 커지는 경우를 방지하기 위해 설정.

{% highlight css %}
div {
    min-width: 300px; /* 아무리 화면이 작아져도 가로 300px이하로는 줄어들지 않음 */
    max-width: 600px; /* 아무리 화면이 커져도 가로 600px이하로는 커지지 않음 */
    min-height: 150px; /* 아무리 화면이 작아져도 세로 150px이하로는 줄어들지 않음 */
    max-height: 400px; /* 아무리 화면이 커져도 세로 400px이하로는 커지지 않음 */
}
{% endhighlight %}

<br/>

## 5) overflow
- 박스 안에 들어간 내용물이 박스보다 큰 경우 어떻게 처리할 지 설정.
- 값: visible, scroll, hidden

a. visible (디폴트 값, 박스 바깥으로 넘치게 보여줌)

{% highlight html %}
<head>
<style>
    .parent{
        border: solid;
        height: 50px;
        overflow: visible;
    }
</style>
</head>

<body>
<div class="parent">
  <p class="child">very very very very very very very very very very very very 
  very very very very very very very very very very very very very very very
  very very very very very very very very very very very very very 
  very very very very very very very very verylong paragraph</p>
</div>
</body>
{% endhighlight %}

<div class="parent" style="height: 50px; border: solid; overflow:visible"><p class="child">very very very very very very very very very very very very 
very very very very very very very very very very very very very
very very very very very very very very very very very very very 
very very very very very very very very very very very long paragraph</p></div>

<br/><br/>

b. scroll (박스에 스크롤 생성)

{% highlight html %}
<head>
<style>
    .parent{
        border: solid;
        height: 50px;
        overflow: scroll;
    }
</style>
</head>

<body>
<div class="parent">
  <p class="child">very very very very very very very very very very very very 
  very very very very very very very very very very very very very very very
  very very very very very very very very very very very very very 
  very very very very very very very very verylong paragraph</p>
</div>
</body>
{% endhighlight %}

<div class="parent" style="height: 50px; border: solid; overflow: scroll;"><p class="child">very very very very very very very very very very very very 
very very very very very very very very very very very very very
very very very very very very very very very very very very very 
very very very very very very very very very very very long paragraph</p></div>

<br/>

c. hidden (넘치는 부분 보여주지 않음)

{% highlight html %}
<head>
<style>
    .parent{
        border: solid;
        height: 50px;
        overflow: hidden;
    }
</style>
</head>

<body>
<div class="parent">
  <p class="child">very very very very very very very very very very very very 
  very very very very very very very very very very very very very very very
  very very very very very very very very very very very very very 
  very very very very very very very very verylong paragraph</p>
</div>
</body>
{% endhighlight %}

<div class="parent" style="height: 50px; border: solid; overflow: hidden;"><p class="child">very very very very very very very very very very very very 
very very very very very very very very very very very very very
very very very very very very very very very very very very very 
very very very very very very very very very very very long paragraph</p></div>

<br/><br/>

참조 : [w3schools.com - CSS Box Model](https://www.w3schools.com/css/css_boxmodel.asp), [codecademy.com - Learn CSS(2. The Box Model)](https://www.codecademy.com/learn/learn-css)