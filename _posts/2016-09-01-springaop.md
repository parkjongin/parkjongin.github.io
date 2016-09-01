---
layout:            post
title:             "스프링 AOP"
category:          Spring
author:            pji
tags:              Spring AOP SpringAOP
---


## Spring AOP
AOP는 관점지향프로그래밍의 약자입니다. Spring에서 AOP를 할때에는 Dynamic Proxy를 이용해서 하게 됩니다. Dynamic Proxy는 동적으로 타겟의 Proxy를 만들어서 Proxy를 통해 AOP를 가능하게 하는 방법입니다. Aspectj는 java가 bytecode로 변환되고 나서 코드를 끼워넣습니다. 하지만 spring은 동적으로 proxy를 통해 접근하므로 많이 어려운점이 없지만 속도가 느리다는 단점이 있습니다.

## AOP의 용어
- Aspect : Aspect는 어던 부가적인 기능을 정의 한다는 의미 입니다. 보통 AOP를 사용하는 곳은 로그, 데이터 처리 속도 등 반복적인 코드가 계속적으로 쓰일 경우 사용합니다. Aspect는 이러한 반복적인 코드가 하는 기능을 정의한다는 의미 입니다.(공통적으로 관심이 있는 사항들..)

- JoinPoint : JoinPoint는 어떤 부가적인 기능을 삽입할 특정 위치를 말합니다.

- PointCut : PointCut은 어떤 클래스의 어느 조인트포인트를 사용할 것인가를 정의합니다.

- Advise : Advise는 각 JointPoint에 삽입되어져 동작할 수 있는 코드를 말합니다.

아래 코드 예제를 보겠습니다.

<figure>

{% highlight java %}
@Aspect
public class ChronometryImpl implements Chronometry{

	long startTime;
	
	@Override
	@Pointcut("@annotation(org.springframework.transaction.annotation.Transactional)")
	public void start() {
		// TODO Auto-generated method stub
		System.out.println("start input");
	}

	@Override
	@Pointcut("@annotation(org.springframework.transaction.annotation.Transactional)")
	public void end() {
		// TODO Auto-generated method stub
		
	}
	
	@Before("@annotation(org.springframework.transaction.annotation.Transactional)")
	public void start_before(){
		startTime = System.currentTimeMillis();
	}
	
	@After("start()")
	public void start_after(){
		System.out.println("처리 시간 : " + (System.currentTimeMillis() - startTime)/1000.0 + "sec");	
	}
	
	
	
}

 
{% endhighlight %}

   <figcaption>aspect 코드</figcaption>
</figure>

위 코드는 처리시간을 측정하기 위한 코드 입니다. @Aspect는 위 ChronometryImpl이 Aspect(어떤 부가적인 기능 정의)로 사용될 것임을 나타냅니다.
그리고 나서 @Pointcut은 어느 조인트 포인트를 사용할 것인가를 정의합니다.(복수 가능) 위 코드에서 조인트 포인트는 @annotation(org.springframework.transaction.annotation.Transactional) 이것이 됩니다. start()는 @Pointcut("@annotation(org.springframework.transaction.annotation.Transactional)")를 재정의한 것입니다. 
advise는 각 조인트포인트에 삽입되어져 동작할 코드들을 나타냅니다.
위 코드에서 보면 @Before("@annotation(org.springframework.transaction.annotation.Transactional)")와 @After("start()")가 있는 것을 확인할 수 있습니다. @Before는 "@annotation(org.springframework.transaction.annotation.Transactional)" 이거 자체가 PointCut이 되어서 따로 PointCut을 정의할 필요가 없습니다. @After는 @Pointcut("@annotation(org.springframework.transaction.annotation.Transactional)")으로 재정의된 start()를 사용하므로 따로 Pointcut을 정의해줘야 합니다.

<figure>
   <img src="/media/img/springaop.png" />
   <figcaption>Spring AOP</figcaption>
</figure>