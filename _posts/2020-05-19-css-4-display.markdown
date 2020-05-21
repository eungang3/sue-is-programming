---
layout: post
title:  "CSS display 이해하기"
date:   2020-05-19 21:00:00 +0900
categories: CSS
---

## 0. display란?
- 가로 공간을 다른 요소와 같이 쓸 것인지 정해주는 프로퍼티. 모든 HTML 요소는 저마다의 디폴트 값 가짐.
- 값 : inline, block, inline-block, flex(다른 포스트에서 집중적으로 다룰 예정)

<br/>

## 1. Inline
- 한 줄에 여러 요소 넣을 수 있음
- 컨텐츠 크기에 맞게 자동으로 박스를 생성하며 height, width 설정해도 못 바꿈. 
- span, strong, a 등의 디폴트 값
- 디폴트 값이 block인 요소에도 쓸 수 있음. 

{% highlight html %}
<head>
<style>
    span {
        background-color: yellow;
        width: 240px; /* 설정해도 소용 없음 */
    }

    div{
        background-color: blue;
        display: inline; /* 디폴트 값을 inline으로 바꿈 */
        width: 240px; /* 이제 설정해도 소용없음 */
    }
</style>
</head>

<body>
<span>I'm span</span>
<div>I'm div displayed as inline element<div>
</body>
</head>
{% endhighlight %}

<br/>

## 2. Block
- 한 줄에 한 요소만 넣을 수 있음.
- 화면 너비 전체를 채우는 게 디폴트지만 width로 조절 가능. 
- p, div, 헤딩 등의 디폴트 값
- 디폴트 값이 inline인 요소에도 쓸 수 있음.

<br/>

## 3. Inline-Block
- 한 줄에 여러 요소 넣을 수 있음
- 기본적으로 컨텐츠 크기에 맞게 자동으로 박스를 생성하지만 height, width 설정 가능.
- img의 디폴트 값



<br/><br/>

참조 :<br/>
[codecademy.com - Learn CSS(3. CSS Display and Positioning)](https://www.codecademy.com/learn/learn-css)<br/>
[w3schools.com - CSS Display Property](https://www.w3schools.com/cssref/pr_class_display.asp)