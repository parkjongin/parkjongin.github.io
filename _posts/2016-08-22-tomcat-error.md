---
layout:            post
title:             "The server does not support version 3.1 of the J2EE Web module specification. 에러가 나는 경우"
category:          Spring
author:            pji
tags:              Tomcat에러, The server does not support version 3.1 of the J2EE Web module specification 에러
---


## 에러 해결 방법
 The server does not support version 3.1 of the J2EE Web module specification. 에러는 현재 Dynamic Web Application 프로젝트를 생성 했을시 Dynamic Web module 버전이 tomcat에서 지원하는 버전과 맞지 않을 경우 발생한다.(이 경우엔 3.1을 지원하지 않는다. 톰캣버전은 7) 이 경우 프로젝트 생성시 tomcat(버전에따라)이 지원하는 Dynamic Web module(톰캣7일 경우 3.0버전)을 선택해주면 된다.


## 에러 화면
<figure>
   <img src="/media/img/tomcat error.png" />
   <figcaption>에러 화면</figcaption>
</figure>

## 에러 해결
<figure>
   <img src="/media/img/tomcat error solution.png" />
   <figcaption>에러 해결</figcaption>
</figure>
