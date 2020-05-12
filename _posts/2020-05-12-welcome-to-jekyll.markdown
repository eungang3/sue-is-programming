---
layout: post
title:  "Jekyll과 Github로 블로그 만들기"
date:   2020-05-12 21:35:27 +0900
categories: Jekyll
---

발생한 문제들:
1. Jekyll이 분명히 설치되었다고 뜨는데 터미널에 입력하면 command not found라고 뜸.
 - rvm으로 Ruby를 다시 깔았더니 설치됨. 

2. 내 컴퓨터에서는 잘 뜨는데 깃헙에 올리면 css가 전혀 적용되지 않음.
 - 새로운 Jekyll 프로젝트 생성하면 자동으로 만들어지는 _config.yml 파일에서 url과 baseurl을 세팅해야 함.
   예) baseurl: "/"
       url: "https://eungang3.github.io/sue-is-programming/" 
 - gh-pages 브랜치에 올려야 깃허브가 지킬 프로젝트로 인식해서 구현해줌. 
 - 내 repo -> 설정 -> GitHub Pages -> Source를 gh-pages 브랜치로 지정해야 함. 