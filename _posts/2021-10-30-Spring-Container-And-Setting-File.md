---
title: "[Spring] 스프링 컨테이너 및 설정 파일"
excerpt: "스프링 컨테이너와 설정 파일"

categories:
  - Spring
tags:
  - [Spring]

toc: true
toc_sticky: true

date: 2021-10-30
last_modified_at: 2021-10-30
---

# 1.  IoC 컨테이너
---

IoC 컨테이너는 각 컨테이너에서 관리할 객체들을 위한 별도의 설정 파일이 있다.

- Servlet 컨테이너 → web.xml
- EJB 컨테이너 → ejb-jar.xml

스프링 프레임워크도 다른 컨테이너와 마찬가지로 자신이 관리할 클래스들이 동록된 XML 설정 파일이 필요하다.

- Spring Bean Configuration File

스프링 설정파일에는 기본적으로 `<beans>` 루트 엘리먼트와 네임스페이스(namespace) 관련 설정들이 추가되어 제공된다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

</beans>
```

간단한 예제를 하나 작성해보자. 앞서 작성했던 [스프링 프레임워크 개요](https://yuunjuu.github.io/spring/SpringFramework/#%EB%8B%A4%ED%98%95%EC%84%B1%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%98%EC%97%AC-%EA%B2%B0%ED%95%A9%EB%8F%84-%EB%82%AE%EC%B6%94%EA%B8%B0) 포스팅의 예제를 참조한다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="a_TV" class="com.spring.ex.A_TV"></bean>
</beans>
```

```java
package com.spring.ex;

public class A_TV implements TV {
	public A_TV() {
		System.out.println("=== A_TV 객체 생성 ===");
	}
	@Override
	public void powerOn() {
		System.out.println("A_TV -- 전원 on");
	}
	@Override
	public void powerOff() {
		System.out.println("A_TV -- 전원 off");
	}
	@Override
	public void volumeUp() {
		System.out.println("A_TV -- 볼륨 up");
	}
	@Override
	public void volumeDown() {
		System.out.println("A_TV -- 볼륨 down");
	}
}
```

```java
package com.spring.ex;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class User {
	public static void main(String[] args) {
		// 1. Spring 컨테이너를 구동한다.
		AbstractApplicationContext factory = new GenericXmlApplicationContext("applicationContext.xml");
		
		// 2. Spring 컨테이너로부터 필요한 객체를 요청(lookup)한다.
		TV tv = (TV)factory.getBean("a_TV", A_TV.class);
		tv.powerOn();
		tv.volumeUp();
		tv.volumeDown();
		tv.powerOff();
		
		// 3. Spring 컨테이너를 종료한다.
		factory.close();
	}
}
```

![1](https://user-images.githubusercontent.com/88693157/139533854-b1f0a997-ca5b-4abd-b883-e835761f1f52.png)

동작 과정은 다음과 같이 표현할 수 있다.

1. User 클라이언트에서 스프링 설정 파일(applicationContext.xml)을 로딩하여 스프링 컨테이너를 구동한다.
   
2. 구동된 스프링 컨테이너 안에 스프링 설정 파일에서 `<bean>`으로 등록된 A_TV 객체를 생성한다.
   
3. User에서 getBean() 메소드를 이용하여 이름이 'a_TV'인 A_TV 객체를 요청(lookup)한다.
   
4. 스프링 컨테이너에서 A_TV 객체를 반환한다.

여기서 중요한 점은 TV를 교체할 때, 스프링 설정 파일 applicationContext.xml 파일만 수정하면 된다는 점이다.

## 스프링 컨테이너의 종류

그렇다면 코드를 다시 한 번 살펴보자. User 클래스에서 스프링 컨테이너를 구동할 때 ApplicationContext 클래스를 사용하였다. 

스프링에서는 BeanFactory와 이를 상속한 ApplicationContext 2가지 유형의 컨테이너를 제공한다.

1. BeanFactory
    
    기능: 스프링 설정 파일에 등록된 `<bean>` 객체를 생성하고 관리하는 가장 기본적인 컨테이너 기능만 제공한다.
    
    특징: 이 때 BeanFactory는 컨테이너가 구동될 때 `<bean>` 객체를 생성하는 것이 아니라, 클라이언트의 요청에 의해서만 생성되는 'lazy loading', 즉 지연 로딩 방식을 사용한다. 따라서 일반적으로는 BeanFactory를 사용하지 않는다.
    
2. ApplicationContext
    
    기능: BeanFactory가 제공하는 `<bean>` 객체 관리 기능 외에 트랜잭션 관리나 메시지 기반의 다국어 처리 등 다양한 기능을 제공한다.
    
    특징: 컨테이너가 구동될 때 `<bean>`에 등록된 클래스들을 객체 생성하는 즉시 로딩(pre-loading) 방식으로 동작한다. 웹 애플리케이션 개발도 지원하기 때문에 일반적으로 ApplicationContext 유형의 컨테이너를 이용한다.
    
    구현 클래스
    
    1) `GenericXmlApplicationContext`: 파일 시스템이나 클래스 경로에 있는 XML 설정 파일을 로딩하여 구동하는 컨테이너
   
    2) `XmlWebApplicationContext`: 웹 기반의 스프링 애플리케이션을 개발할 때 사용하는 컨테이너

# 2.  스프링 XML 설정

---

## `<beans>` 루트 엘리먼트

스프링 컨테이너는 `<bean>` 저장소에 해당하는 XML 설정 파일을 참조하여 `<bean>`의 생명주기를 관리하고 여러 서비스를 제공한다. 따라서 스프링 프로젝트에서 가장 중요한 역할을 하며, 이 설정 파일을 정확하게 작성하고 관리하는 것이 중요하다.

## `<import>` 엘리먼트

스프링 기반의 애플리케이션은 단순히 `<bean>` 등록 외에도 트랜잭션 관리, 예외 처리, 다국어 처리 등 다양한 설정이 필요하다. 이러한 설정 파일들을 하나로 통합할 때 `<import>`를 사용한다.

```xml
<beans>
	<import resource="context-datasource.xml">
	<import resource="context-transaction.xml">
</beans>
```

## `<bean>` 엘리먼트

스프링 설정 파일에 클래스를 등록하려면 `<bean>`을 사용한다. class 속성에는 클래스의 정확한 경로와 이름을 지정해야 한다. id 속성에는 클라이언트가 컨테이너에 객체를 요청할 때 사용되므로 유일한 이름을 사용해야 한다. 이 때 이름에는 숫자나 공백, 특수기호가 포함되어서는 안 된다. 만약 특수기호가 포함된 아이디를 사용할 경우에는 name 속성을 사용한다.

1. init-method
    
    스프링 컨테이너에서 스프링 설정 파일에 등록된 클래스를 객체로 생성할 경우에는 기본 생성자를 호출한다. 따라서 객체를 생성한 후에 멤버변수 초기화 작업이 필요하면 init-method 속성을 사용한다.
    
2. destroy-method
    
    init-method와 마찬가지로 스프링 컨테이너에서 객체를 삭제하기 직전에 호출될 임의의 메소드를 지정할 수 있다.

    **init-method와 destroy-method 예제**

    ```xml
    <bean id="a_TV" class="com.spring.ex.A_TV" init-method="initMethod" destroy-method="destroyMethod"></bean>
    ```

    ```java
    package com.spring.ex;

    public class A_TV implements TV {
      public void initMethod() {
        System.out.println("객체 초기화 작업...");
      }
      public void destroyMethod() {
        System.out.println("객체 삭제 전 처리...");
      }
      public A_TV() {
        System.out.println("=== A_TV 객체 생성 ===");
      }
      // 생략
    }
    ```

    ![2](https://user-images.githubusercontent.com/88693157/139533975-835396b3-a155-428a-9b71-e6723f35a482.png)

3. lazy-init
    
    ApplicationContext는 즉시 로딩 방식을 사용하지만 어떤 `<bean>`은 자주 사용되지 않으면서 메모리를 많이 차지하여 시스템에 부담을 주는 경우가 있다. 따라서 컨테이너 구동 시점이 아닌 `<bean>` 객체가 사용되는 시점에 객체를 생성하도록 lazy-init 속성을 사용할 수 있다.
    
    ```xml
    <bean id="a_TV" class="com.spring.ex.A_TV" lazy-init="true" />
    ```
    
4. scope
    
    프로그램을 개발할 때 생성되는 수많은 객체 중에는 하나만 생성되어도 상관없는 객체들이 있다. 하나의 객체만 생성하여 유지하려면 객체를 생성하고 주소를 복사해서 재사용하는 방법이 있지만, 이는 쉽지 않은 방법이다. 
    
    스프링 컨테이너는 컨테이너가 생성한 bean을 어느 범위에서 사용할 수 있는지를 지정할 수 있는데 이 때 scope 속성을 사용한다. 이 scope 속성값의 기본값은 싱글톤으로, 해당 bean이 스프링 컨테이너에 의해 하나만 생성되어 운용되도록 한다. singleton이 아닌 prototype으로 지정할 경우에는 스프링 컨테이너는 해당 `<bean>`이 요청될 때마다 매번 새로운 객체를 생성하여 반환한다.
    
    ```xml
    <bean id="a_TV" class="com.spring.ex.A_TV" scope="singleton" />
    ```
    
    ![3](https://user-images.githubusercontent.com/88693157/139534017-67739965-1013-4191-9c68-f39900022d29.png)
    
    ```xml
    <bean id="a_TV" class="com.spring.ex.A_TV" scope="prototype" />
    ```

    ![4](https://user-images.githubusercontent.com/88693157/139534019-09f7439a-322b-4e82-be3f-78d89fcb46a8.png)


# 참고
---
- 스프링 퀵 스타트