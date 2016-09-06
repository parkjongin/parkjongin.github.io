---
layout:            post
title:             "IOC컨테이너, ApplicationContext, BeanFactory Spring"
category:          Spring
author:            pji
tags:              IOC컨테이너 ApplicationContext Spring BeanFactory
---


## IOC컨테이너, ApplicationContext, BeanFactory
IoC컨테이너와 ApplicationContext, BeanFactory가 의미하는 것은 비슷하다. IoC컨테이너는 BeanFactory라고 불리기도 한다.
BeanFactory는 빈의 생성과 제어의 관점에서 이야기를 하는 것이고 ApplicationContext는 스프링이 제공하는 Application 지원 기능을 모두 포함해서 이야기 하는 것이다. 
스프링에서 핵심기능은 ApplicationContext이다. 우리가 흔히 xml로 정의하는 ApplicationContext(RootContext)를 설정정보로 참조한다. ApplicationContext에서 Bean의 생성, 조회, 등록 등을 담당한다. BeanFactory를 상속받는다. 따라서 BeanFactory의 중요 기능인 Bean 생성, 조회, 등록을 그대로 받고 여기에 스프링에 제공하는 부가기능을 추가로 제공한다.


<figure>
   <img src="/media/img/applicationContext.png" />
   <figcaption>ApplicationContext 동작방식</figcaption>
</figure>

- ApplicationContext는 @Configuration 어노태이션이 붙은 자바 파일이나, xml로 만든 <beans로 시작하는 appcontext를 설정정보로 등록하고 @Bean이 붙은 메소드의 이름을 가져와 빈 목록을 만든다. 
- 클라이언트가 ApplicationContext의 getBean() 메소드를 호출하면 자신의 빈 목록에서 요청한 이름이 있는지 찾고, 있다면 빈을 생성하는 메소드를 호출해서 오브젝트를 생성시킨 후 클라이언트에 돌려준다.

## ApplicationContext와 BeanFactory
ApplicationContext를 사용하면 BeanFactory사용보다 더 범용적이고 유연하게 IoC기능을 확장해서 사용할 수 있다.

### 장점

- 클라이언트는 구체적인 팩토리 클래스를 알 필요가 없다.
- 종합 IoC 서비스를 제공해 준다.
- 빈을 검색하는 다양한 방법을 제공한다.


토비의 Spring 3.0을 참고하여 작성하였습니다.