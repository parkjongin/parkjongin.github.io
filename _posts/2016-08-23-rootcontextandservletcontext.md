---
layout:            post
title:             "Application Context와 Servlet Context"
category:          Spring
author:            pji
tags:              Spring ServletContext RootContext Web.xml
---


## Root Context와 Servlet Context
Servlet Context는 서블릿이 서블릿 컨테이너와 통신하기 위한 메서드들을 기록한 클래스 입니다. Root Context(Application Context) 또한 같은 역할을 한다고 생각합니다. Root Context는 Servlet Context의 부모 자식 관계입니다. Root Context가 Servlet Context의 부모 위치에 있으며, Root Context를 상속받아 Servlet Context가 생성됩니다. 따라서 Root Context는 Servlet Context의 자원을 사용할 수 없지만 Servlet Context는 Root Context의 자원을 사용할 수 있습니다.
Root Context는 web.xml에서 listener를 통해 부모 Context로 등록할 수 있습니다. 
Context 로드 순서는 root->servlet 순으로 진행됩니다.
보통 Controller를 제외한 Component를 Root Context에 등록해서 사용하고 Controller류의 Component는 Servlet에 등록해서 사용합니다.
그 이유는 여러가지가 있지만 제가 겪은것(아직 추측입니다.)은 각 서블릿마다 컨트롤러를 따로 가지고 있어야 하고 만약 Root Context와 중복된 bean을 정의하면 우선순위는 servlet이 됩니다. 하지만 Context 로드 순서는 Root Context가 먼저 로드 되기 때문에 Root Context에 있는 bean은 DI가 되어 있지만 나중에 로드되는 Servlet Context는 이미 Root Context 에서 등록된 중복 bean을 상속받아 override하는 과정에서 DI가 제대로 되지 않는 결과가 나지 않았나 싶습니다. 제대로 DI가 되지 않은 Servelt Context의 bean이 막상 호출되었을때 Root Context의 bean보다 우선순위에서 앞서기 때문에 제대로 DI가 되지 않은 bean이 호출되어서 오류가 났던 것 같습니다.
아직은 추측단계 이지만 auto component scan과정에서 에러가 발생한 것을 서블릿에만 controller등록을 해주어 해결을 했던 경험이 있습니다. 확실한 이유를 아시는 분은 알려주세요.
