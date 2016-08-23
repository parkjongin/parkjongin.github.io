---
layout:            post
title:             "Spring에서 자바 bean 메타설정, xml bean 메타설정"
category:          Spring
author:            pji
tags:              Spring bean xmlbean javabean
---

## Bean
자바 인스턴스

## Spring Bean Factory
Spring에서는 Bean을 기본적으로 싱글톤으로 인스턴스를 생성해서 관리한다. IoC컨테이너, 스프링컨테이너로 불리기도 하는것 같다. java reflection 기술을 이용해서 등록을 해준다.

## JAVA Bean
<figure>

{% highlight java %}

@Configuration
public class bean{
	@Bean
	public classType dataSource(){
		classType dataSource = new classType();
		dataSource.setid("id");
		dataSource.setpw("pw");
		dataSource.setDriverClass(com.db.driver.class);
		
		return dataSource;
	}
}


{% endhighlight %}

   <figcaption>spring java bean 메타설정 예</figcaption>
</figure>

- Java에서는 @Configuration 어노태이션과 @Bean 어노태이션이 함께 사용되면 빈 메타정보를 자바로 작성할 수 있게된다. 


## XML Bean
<figure>
{% highlight xml %}
<beans>
	<bean id="datasource" class=classpath:bean>
		<property name="driverClass" value="com.db.driver.class"/>
		<property name="pw" value="pw"/>
		<property name="id" value="id"/>
	</bean>
</beans>


{% endhighlight %}
   <figcaption>spring xml bean 메타설정 예</figcaption>
</figure>
- XML에서는 bean태그로 빈 메타정보를 작성할 수 있다.
