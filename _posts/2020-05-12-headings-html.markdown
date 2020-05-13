---
layout: post
title:  "시멘틱 요소를 사용하여 웹 접근성을 높이는 8가지 방법"
date:   2020-05-12 21:35:27 +0900
categories: HTML
---

# 시멘틱이란? 

시멘틱은 의미론적이라는 뜻이다. 시멘틱 요소는 컨텐츠의 의미에 맞게 사용하라고 만들어진 요소이다. 시멘틱 요소는 검색 엔진이 내 웹페이지를 크롤링, 인덱싱하기 쉽게 해주고 장애가 있는 유저의 접근성도 높여준다. 

시멘틱 요소가 갖고 있는 의미에 따라 html을 구성하면 검색엔진이나 스크린 리더에게 어디에 중요한 내용이 있는지, 정보가 어떻게 구성되어있는지 말해줄 수 있다. 기계뿐만 아니라 다른 개발자가 내 코드를 이해하는 데도 도움을 줄 수 있다.

예를 들어 h1 태그는 "여기에 가장 중요한 정보가 있다"고 말해주는 요소이다. 검색 엔진은 h1에 든 내용을 인덱싱해두었다가 검색결과로 보여준다. h1 태그로 컨텐츠의 가장 중요한 부분을 감싸야 검색 엔진에게 내가 주고싶은 가장 중요한 정보를 줄 수 있다. 다른 개발자가 내 코드를 봤을 때도 h1을 보면 어디가 중요한 부분인지 쉽게 알 수 있다. 

그럼 구체적으로 시멘틱 요소를 어떻게 사용하면 좋을지 알아보자. 

## 1. img태그에 alt 속성 부여하기

- 활용: 해당 이미지를 설명하는 간단한 글 입력. "이미지가 없을 때 이 글을 띄워줘"라는 의미.
   예) <img src="foo.jpeg" alt="Picture of a cat">

- 이유: 이미지를 로드할 수 없을 때 브라우저가 대신 화면에 나타낼 수 있는 정보를 제시함
       시각장애인이 사용하는 스크린 리더가 이미지에 대한 정보도 읽을 수 있게 함
       검색 엔진이 수집할 수 있는 정보 제공

- HTML5부터는 의무적으로 작성해야 함. 작성하지 않을 시 장애인 차별금지법에 근거한 법적인 문제가 생길 수 있음.

- 예외 : 순수하게 장식적인 이미지라면 alt에 아무것도 넣지 않아도 됨. 
  예) <img src="foo.jpeg" alt="">


## 2. 의미에 맞게 헤딩 태그 사용하기

- 헤딩 태그는 컨텐츠에 구조를 부여하는 의미론적 요소. 컨텐츠의 구조에 맞게 헤딩 태그 써야 함.
  단순히 글씨 크기를 조절하고 싶다면 헤딩 태그를 쓰는 게 아니리 css에서 조절해야 함.

- 활용 : h1 - h6까지 있음. h1 다음에는 h2, h2 다음에는 h3.. 이런 식으로 위계에 맞게 써야 함.
        한 웹페이지에는 무조건 하나의 h1태그가 있어야 하고 단 하나만 있어야 함. 
  
  예) <h1>면의 종류</h1>
        <h2>국수면</h2>
           <h3>메밀국수면</h3>
           <h3>쌀국수면</h3>
        <h2>파스타면</h2>
     <h2>우동면</h2>

- 이유 : 검색 엔진은 헤딩 태그에 든 내용을 크롤링, 인덱싱함. 컨텐츠 내용을 핵심적으로 요약한 제목 부분에 헤딩을 써야 내가 원하는 정보를 검색 엔진에게 줄 수 있음. 장애인 보조기기(스크린 리더 등)가 내용 해석하는 데 도움.

## 3. main, header, footer, nav, article, section 사용하기

장애 보조기기 사용하는 유저가 페이지 탐색하기 쉽게 해줌 (예: 바로 원하는 내용으로 갈 수 있게 해줌, 더 나은 페이지 요약 제공 등). div과 비슷한 방식으로 렌더링됨. 

    1) main 태그 
    - 메인이 되는 내용을 태그로 감싸기. 한 페이지에 단 하나만 있어야 함.

    2) header 태그 
    - <head>와는 다름, 도입부나 여러 페이지에서 반복되는 컨텐츠에 사용. 

    3) footer 태그 
    - 웹페이지 하단에 반복되는 정보 표기할 때 사용 (예: 카피라이트)

    4) article 태그
    - 그 자체로 완결성 갖는 독립적인 컨텐츠에 사용 

    5) section 태그
    - 연관된 주제를 갖는 컨텐츠를 묶을 때 사용. 컨텐츠 간 아무 연관이 없다면 div 사용. 
    - article이 책이라면 section은 챕터 (FCC 참조: https://www.freecodecamp.org/learn/responsive-web-design/applied-accessibility/wrap-content-in-the-article-element)

    6) nav 태그
    - 메인 네비게이션 바에 사용


## 4. audio 태그 사용 시 캡션이나 설명, 링크 제공하기
  cf) audio 태그 활용:
  <audio id="foo" controls>
  <source src="audio/bar.mp3" type="audio/mpeg" />
  </audio>


## 5. figure 태그 사용하기
  - 활용 : 시각적인 요소(이미지, 차트 등)를 감싸고 <figcaption>으로 캡션 제공하기
    예) <figure>
        <img src="foo.jpeg" alt="Picture of a cat drinking milk">
        <figcaption>
        A cat is drinking milk.
        </figcaption>
        </figure>

  - 이유 : 연관된 요소를 묶고 대안이 되는 텍스트를 제시함으로써 접근성을 두 배 높임
  
## 6. label 태그에 for 속성 제공하기
 - 활용 : form control의 id와 같은 값 입력
   예) <form>
        <label for="name">이름</label>
        <input type="text" id="name" name="name>
      </form>
 - 이유 : 어떤 텍스트가 어떤 form control과 연관되는지 스크린 리더가 읽을 수 있게 함, 
 form control이 작을 때(예: 라디오 버튼)클릭하기 어려운데, label 영역 지정하면 label 클릭해서 form control 조작 가능함.     

## 7. 라디오 버튼을 fieldset 태그로 감싸기
 - 활용 : fieldset 태그로 라디오 버튼 모두 감싸고 legend 태그로 각 선택지 설명 감싸기
   예) <form>
        <fieldset>
        <legend>하나를 고르세요</legend>
        <label for="one">첫번째</label>
        <input id="one" type="radio" name="items" value="first">
        <label for="two">두번째</label>
        <input id="two" type="radio" name="items" value="second">
        </fieldset>
       </form>

## 8. time 태그에 datetime 속성 부여하기
  - 활용 : time 태그의 datetime 속성에 표준시 입력
    예) 다음 모임은 <time datetime="2020-05-12">5월 12일</time>에 있을 예정입니다.
  - 이유 : 장애인 보조기기(스크린 리더 등)가 내용 해석하는 데 도움


참조:
https://www.freecodecamp.org/learn - Applied Accessibility 항목
https://poiemaweb.com/html5-semantic-web