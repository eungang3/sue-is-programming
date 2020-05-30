---
layout: post
title:  "CSS Multi-Column Layout 이해하기"
date:   2020-05-30 00:00:00 +0900
categories: CSS
---

## 0. Multi-Column Layout이란?
- 많은 양의 텍스트가 있을 때 여러 단으로 나누어 보여주는 레이아웃 방식. 
- grid, flexbox와 달리 한 단에 있는 텍스트가 넘치면 다른 단으로 자동으로 흐름.
- block layout mode의 확장형. 

<br/>

## 1. Multi-column Layout 정의하기 
### 1) Column-count
- 단을 몇 개로 할 지 설정하는 프로퍼티.
{% highlight css %}
div {
    column-count: 2;
} 
{% endhighlight %}

<br/>

### 2) Column-width
- 단의 최소 너비를 몇으로 할 지 설정하는 프로퍼티.
- % 제외한 모든 단위 사용 가능. (rem, em 권장) 
- 현재 브라우저 너비에 최소 너비 column이 몇 개 들어갈 지 자동으로 계산해서 구현. 
- column-count와 동시에 사용한 경우, column-count에 지정된 값이 최대 가능한 단의 개수. 

{% highlight css %}
div {
    width: 100%;
    column-width: 10rem; 
} 
{% endhighlight %}

<br/>

### 3) Columns
- column-count, column-width를 줄여쓰는 프로퍼티.
{% highlight css %}
div {
    columns: 20rem 3; 
} 
{% endhighlight %}

{% highlight css %}
div {
    columns: 3; 
} 
{% endhighlight %}

<br/>

## 2. Multi-column spanning
- 어떤 요소가 얼마나 단을 차지하게 할 지 설정. 
- 값 : none(기본값, 1개 단만 차지), all(모든 단 차지)

{% highlight html %}
<head>
<style> 
div {
  column-count: 3;
}

h2 {
  column-span: all;
}
</style>
</head>

<body>
<div>
Lorem ipsum dolor sit amet, consectetuer adipiscing elit, 
sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna 
aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud 
exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex 
ea commodo consequat. Duis autem vel eum iriure dolor in hendrerit 
in vulputate velit esse molestie consequat,
<h2>Lorem Ipsum Dolor Sit Amet</h2> vel illum dolore eu feugiat nulla 
facilisis at vero eros et accumsan et iusto odio dignissim qui 
blandit praesent luptatum zzril delenit augue duis dolore te feugait 
nulla facilisi. Nam liber tempor cum soluta nobis eleifend option congue 
nihil imperdiet doming id quod mazim placerat facer possim assum.
</div>
</body>
{% endhighlight %}

<br/>

## 3. Multi-column 스타일링하기
### 1) Column-gap
- 단 사이 공간 설정.
- 기본값은 normal(=1em).
{% highlight css %}
div {
    columns: 3; 
    column-gap: 10rem;
} 
{% endhighlight %}

<br/>

### 2) Column rules
- multi column container 안쪽의 모든 column에 같은 스타일 설정 가능. 
- 공간 차지하지 않음(gap 위에 겹쳐서 보임)

#### a. column-rule-style
- 단 사이에 선 표시할 것인지, 어떤 선으로 표시할 것인지 지정. 
- 값 : none(기본값), dotted, solid, double, ridge 등

{% highlight html %}
<head>
<style>
div {
  column-width: 10rem;
  column-rule-style: solid;
}
</style>
</head>

<body>
<div>
Lorem ipsum dolor sit amet, consectetuer adipiscing elit, 
sed diam nonummy nibh euismod tincidunt ut laoreet dolore 
magna aliquam erat volutpat. Ut wisi enim ad minim veniam, 
quis nostrud exerci tation ullamcorper suscipit lobortis nisl 
ut aliquip ex ea commodo consequat. Duis autem vel eum iriure dolor 
in hendrerit in vulputate velit esse molestie consequat, 
vel illum dolore eu feugiat nulla facilisis at vero eros et 
accumsan et iusto odio dignissim qui blandit praesent luptatum 
zzril delenit augue duis dolore te feugait nulla facilisi. 
Nam liber tempor cum soluta nobis eleifend option congue nihil 
imperdiet doming id quod mazim placerat facer possim assum.
</div>
</body>
{% endhighlight %}

<div style="column-width: 10rem;column-rule-style: solid;">
Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi. Nam liber tempor cum soluta nobis eleifend option congue nihil imperdiet doming id quod mazim placerat facer possim assum.
</div>

<br/>

#### b. column-rule-width
- 단 사이의 선 굵기 설정.

<br/>

#### c. column-rule-color
- 단 사이의 선 색상 설정.

<br/>

#### d. column-rule
- column-rule-width, column-rule-style, column-rule-color 동시에 지정하는 프로퍼티.
{% highlight css %}
div {
    columns: 3; 
    column-rule: 1px solid red;
} 
{% endhighlight %}


<br/><br/>
참조 :<br/>
[W3Schools.com - CSS Multiple Columns](https://www.w3schools.com/css/css3_multiple_columns.asp)<br/>
[MDN web docs - Multi-column layouts](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Columns)