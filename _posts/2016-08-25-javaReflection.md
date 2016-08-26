---
layout:            post
title:             "JAVA Reflection"
category:          Spring, JAVA
author:            pji
tags:              Reflection JAVARecflection
---


## 리플렉션이란?
 '컴퓨터 프로그램에서 런타임 시점에 사용되는 자신의 구조와 행위를 관리(type introspection)하고 수정할 수 있는 프로세스를 의미한다. (type introspection)은 객체 지향 프로그램언어에서 런타임에 객체의 형(type)을 결정할 수 있는 능력을 의미한다.' 라고 위키에 되어 있다.

 자바는 컴파일 과정 다음 바이트코드로 생성된 클래스 정보를 이용해서 reflection을 하게 된다. 동적으로 인스턴스를 생성하게되는 것이다. reflection을 이용하면 클래스 이름을 알면 동적으로 인스턴스를 생성할 수 있고, 메소드호출 및 멤버변수도 알 수 있다. private멤버변수 또한 접근 가능하다.

 reflection기술은 보통 라이브러리를 만들 때 사용할 수 있다. 예를 들면 자료형에 상관없이 json객체로 만들어주는 기능이 필요하다고 생각해보자.
 자료형에는 우리가 모델로 정의한 클래스가 있을 수도 있고 형태가 다양할 것이다. 이럴경우 자바 리플렉션을 이용해서 json객체로 만들어줄 수 있다.

## JAVA Reflection을 이용한 JSON객체 생성

<figure>
{% highlight JAVA %}

public class Album {
	Integer id;
	String title;
	String nation;

	public Integer getId() {
		return id;
	}
	public void setId(Integer album_id) {
		this.id = id;
	}
	public String getTitle() {
		return title;
	}
	public void setTitle(String title) {
		this.title = title;
	}
	public String getNation() {
		return nation;
	}
	public void setNation(String nation_cd) {
		this.nation = nation;
	}
}

{% endhighlight %}
   <figcaption>model class file</figcaption>
</figure>

- album이라는 클래스를 정의하고 멤버변수와 메소드를 정의했다.


<figure>
{% highlight JAVA %}

	public String generateJsonAndToString(Object obj){
		JSONObject json = new JSONObject();
		char[] methodNameArr = null;
		String methodName = null;
		Method method = null;
		
		for (Field field : obj.getClass().getDeclaredFields()){ 
			// reflection을 이용해서 멤버변수의 이름을 구한다.
			try {
				methodNameArr = field.getName().toCharArray(); 
				//메소드 이름이 멤버변수 이름의 첫 알파벳이 대문자로 바뀐 것이라고 가정하고 필드이름을 구해서 넣어준다.
				methodNameArr[0] = (char)((methodNameArr[0] - 'a') + 'A'); 
				// 첫 알파벳을 대문자로 바꿔준다.
				methodName = "get" + new String(methodNameArr); 
				// 앞에 get을 추가해서 getMethod가 되도록 한다.

					try {
						method = obj.getClass().getMethod(methodName); 
						// 메소드 오브젝트에 reflection을 이용해서 메소드객체를 담는다.
						json.put(field.getName(), method.invoke(obj)); 
						// 메소드 실행
					} catch (NoSuchMethodException | SecurityException | IllegalAccessException | InvocationTargetException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}


			} catch (IllegalArgumentException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}

		}

		return json.toString(); json 스트링 형태로 반환.
	}

{% endhighlight %}
   <figcaption>리플렉션을 이용해서 object를 json string으로 변환하는 함수코드</figcaption>
</figure>

- 매개변수를 Object형으로 받고 어떠한 자료형이 오더라도 사용이 가능하도록 한다. Object 클래스에서 getClass 메소드를 이용해서 reflection한다.(주석참고)