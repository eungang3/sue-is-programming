---
layout: post
title:  "CSS position 이해하기"
date:   2020-05-18 23:35:27 +0900
categories: CSS
---

## 0. position이란?
- 요소를 어떻게 위치시킬지 정해주는 프로퍼티.
- 값 : static(디폴트), relative, absolute, fixed

<br/>

## 1. static
- 디폴트 값. HTML 플로우대로 구현(위에서 아래로, 좌측에서 우측으로)

{% highlight html %}
<head>
<style>
    .box1 {
        background-color: yellow;
        width: 240px;
        height: 240px;
    }

    .box2 {
        background-color: blue;
        width: 120px;
        height: 120px;
    }
</style>
<body>
<div class="box1"></div>
<div class="box2"></div>
</body>
</head>
{% endhighlight %}

![position1](https://eungang3.github.io/sue-is-programming/assets/position1.jpg)

<br/>

## 2. relative
- 자기가 디폴트 값 static인 경우 위치했을 곳을 기준점으로 잡아 이동시킴.
- 오프셋 프로퍼티 top, bottom, left, right 값 지정해서 어디에 위치시킬 지 정함
- static일 때는 오프셋 프로퍼티 값 있어도 적용 안됨.

{% highlight html %}
<head>
<style>
    .box1 {
        background-color: yellow;
        width: 240px;
        height: 120px;
    }

    .box2 {
        background-color: blue;
        width: 240px;
        height: 120px;
        position: relative;
        top: 40px; /* 자기의 원위치 상단에서 40px 떨어진 곳에 위치 */
        left: 50px; /* 자기의 원위치 좌측에서 50px 떨어진 곳에 위치 */
    }
</style>
<body>
<div class="box1"></div>
<div class="box2"></div>
</body>
</head>
{% endhighlight %}

![position2](https://eungang3.github.io/sue-is-programming/assets/position2.jpg)

<br/>

## 3. absolute
- position이 디폴트 static이 아닌 부모 중 가장 가까운 부모를 기준점으로 잡아 이동시킴. 
- 모든 부모의 position이 static이라면 html을 기준점으로 잡음.
- 부모로 잡고싶은 요소의 position은 주로 relative로 설정.
- 웹페이지의 플로우에서 제거됨. (다른 요소들은 absolute 요소가 없는 것처럼 행동함.) 

{% highlight html %}
<head>
<style>
    .parent {
        background-color: yellow;
        width: 240px;
        height: 120px;
        position: relative; /* .child의 기준점이 됨 */
    }

    .child {
        background-color: blue;
        width: 240px;
        height: 120px;
        position: absolute;
        top: 40px; /* .parent div의 상단에서 40px 떨어진 곳에 위치 */
        left: 50px; /* .parent div의 좌측에서 50px 떨어진 곳에 위치 */
    }
</style>
<body>
<div class="parent">
    <div class="child"></div>
</div>

</body>
</head>
{% endhighlight %}

![position3](https://eungang3.github.io/sue-is-programming/assets/position3.jpg)

## 4. fixed
- viewport를 기준점으로 잡음. 
- position이 fixed인 요소는 absolute와 달리 스크롤을 올리든 내리든 그 자리에 계속 있음.

<br/>

## + z-index
- 여러 요소가 겹칠 때 무엇을 앞에 놓을지 정해줌.
- 기본값은 0, 숫자가 클수록 앞으로 나감.
- 부모 값이 낮으면 자식 값이 높아도 다른 부모 값은 못 이김. (stacking context 고려해야 함)

{% highlight html %}
<head>
<style>
div {
  width: 240px;
  height: 120px;
}

.parent1 {
  background-color: yellow;
  position: relative;
  z-index: 1;
}

.parent2 {
  position: relative;
  background-color: green;
  position: relative;
  z-index: 2;
}

.child1{
  position: absolute;
  background-color: blue;
  width: 120px;
  height: 120px;
  top: 30px;
  left: 50px;
  /* z-index: 3;이라도 부모가 1이라서 맨 위에 올라오지 않음*/
}

.child2{
  position: absolute;
  background-color: red;
  width: 120px;
  height: 120px;
  top: -30px;
  left: 70px;
}
</style>
</head>

<body>
<div class="parent1">
 <div class="child1">
 </div>
</div>

<div class="parent2">
<div class="child2">
 </div>
</div>
</body>
{% endhighlight %}

![position4](https://eungang3.github.io/sue-is-programming/assets/position4.jpg)

<br/><br/>

참조 : [w3schools.com - CSS Position Property](https://www.w3schools.com/cssref/pr_class_position.asp)<br/>
[codecademy.com - Learn CSS(3. CSS Display and Positioning)](https://www.codecademy.com/learn/learn-css)<br/>
[생활코딩 CSS 수업 - 포지션](https://opentutorials.org/course/2418/13414)<br/>
[부스트코스 - 초보자를 위한 HTML&CSS 동작과 원리 - Layout 설정](https://www.edwith.org/htmlcss/lecture/16616/)