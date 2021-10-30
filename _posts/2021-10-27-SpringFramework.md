---
title: "[Spring] 스프링 프레임워크 개요"
excerpt: "프레임워크, 스프링 프레임워크, Ioc 컨테이너"

categories:
  - Spring
tags:
  - [Spring]

toc: true
toc_sticky: true

date: 2021-10-27
last_modified_at: 2021-10-27
---

# 1.  프레임워크 개념
---

```
✔ 틀, 체계 라는 의미의 프레임워크는 소프트웨어 관점에서 골격 코드라 할 수 있다.
```
시스템을 개발하는 과정에서 대부분의 개발자들은 산출물에 입각해서 개발하므로 아키텍처의 일관성이 잘 유지된다. 하지만 유지보수 과정에서 인력과 시간 부족으로 산출물이 무시되거나 개발자들의 경험에 의존하여 유지보수가 진행되는 경우가 많다. 프레임워크는 기본적인 뼈대를 제공하므로, 개발자들은 그 뼈대 위에 살만 덧붙이는 작업을 하면 되는 것이다.

**프레임워크의 장점**

1. 빠른 구현 시간
    
    프레임워크는 아키텍처에 해당하는 골격 코드를 제공하므로 개발자는 비즈니스 로직만 구현하면 된다. 따라서 제한된 시간 안에 많은 기능을 구현할 수 있다.
    
2. 쉬운 관리
    
    같은 프레임워크가 적용된 애플리케이션들은 아키텍처가 같기 때문에 관리하기가 쉽다.
    
3. 개발자들의 역량 획일화
   
4. 검증된 아키텍처의 재사용과 일관성 유지



# 2.  스프링 프레임워크란
---

스프링 프레임워크가 등장하기 이전에 자바 기반의 엔터프라이즈 애플리케이션은 EJB(Enterprise Java Beans)로 개발되었다. 그러나 EJB는 스펙이 너무 복잡하여 학습과 개발 및 유지보수에 많은 시간과 노력이 필요하며, EJB로 만들어진 컴포넌트들은 고가의 WAS에서 실행된다는 단점이 있다.

반면 로드 존슨이라는 사람이 2004년 개발한 스프링 프레임워크는 평범한 POJO(Plain Old Java Object)를 사용하기 때문에 EJB에 비해 간단하다. 여기서 POJO는 평범한 옛날 자바 객체를 의미한다. Not POJO에는 대표적으로 Servlet 클래스가 있다. 서블릿 클래스는 반드시 규칙에 맞게 클래스를 만들어야 실행할 수 있다.

스프링 프레임워크는 'IoC와 AOP를 지원하는 경량의 컨테이너 프레임워크'이다.

1. 경량(LightWeight)
    
    스프링 프레임워크는 '가볍다'는 특징이 있다. 스프링은 여러 개의 모듈에 각각 하나 이상의 JAR 파일로 구성되어 있어 개발과 실행이 모두 가능하다. 따라서 스프링으로 만든 애플리케이션의 배포 역시 쉽고 빠르다는 장점이 있다.
    
2. 제어의 역행(Inversion of Control, IoC)
    
    스프링은 제어의 역행을 통해 객체 간의 낮은 결합도를 유지한다. 제어의 역행이 적용되기 전에는 애플리케이션 수행에 필요한 객체의 생성이나 객체와 객체 사이의 의존 관계를 개발자가 직접 자바 코드로 처리했었다. 이런 상황에서는 의존 관계에 있는 객체를 변경할 때 반드시 자바 코드를 수정해야 한다. 그러나 제어의 역행이 적용되면 객체 생성과 객체와 객체 사이의 의존 관계를 자바 코드로 직접 처리하는 것이 아니라 컨테이너가 대신 처리한다. 결과적으로 의존관계가 명시되지 않으므로 결합도가 떨어져 유지 보수가 편리해지는 것이다.
    
3. 관점지향 프로그래밍(Aspect Oriented Programming, AOP)
    
    관점지향 프로그램은 핵심 기능과 공통 기능을 분리하여 응집도가 높게 개발할 수 있도록 한다. 공통으로 사용하는 기능들은 외부의 독립된 클래스로 분리하고, 해당 기능을 프로그램 코드에 명시하지 않고, 선언적으로 처리하여 적용한다. 이렇게 되면 공통 기능을 분리하여 관리할 수 있으므로 응집도가 높은 컴포넌트를 생성하고 유지보수가 쉬워진다.
    
4. 컨테이너(Container)
    
    컨테이너는 특정 객체의 생성과 관리를 담당하며 객체 운용에 필요한 다양한 기능을 제공한다.
    

# 3. IoC 컨테이너
---

스프링 프레임워크를 이해하는데 가장 중요한 개념이 바로 컨테이너이다. 대부분의 컨테이너는 비슷한 구조와 동작 방식을 가지고 있으므로 서블릿 컨테이너를 통해 스프링 컨테이너의 동작 방식을 유추해볼 수 있다.

```java
public class HelloServlet extends HttpServlet {
	public HelloServlet() {
		System.out.println(">>> HelloServlet 객체 생성");
	}
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("doGet() 메소드 호출");
	}
}
```

서블릿 클래스는 web.xml 파일에 자동으로 등록된다.

```xml
<web-app>
	<servlet>
		<servlet-name>hello</servlet-name>
		<servlet-class>hello.HelloServlet</servlet-class>
	</servlet>
	<servlet-mapping>
		<servlet-name>hello</servlet-name>
		<url-pattern>/hello.do</url-pattern>
	</servlet-mapping>
</web-app>
```
web.xml의 설정은 /hello.do라는 URL 요청을 전송하면, hello라는 이름으로 등록된 hello.HelloServlet 클래스를 찾아 객체를 생성하고 실행한다는 설정이다.

HelloServlet 프로그램을 실행하면 아래와 같은 메시지가 콘솔에 출력되고, web.xml 설정대로 객체가 생성되고 실행되는 것을 확인할 수 있다.
```
>>> HelloServlet 객체 생성
doGet() 메소드 호출
```
서블릿은 자바로 만들어진 클래스로 반드시 객체 생성을 해야 객체가 가진 메소드도 호출할 수 있다. 그런데 작성된 소스 코드에서는 객체 생성 코드나 doGet() 메소드의 호출이 보이지 않는다. 그렇다면 이 서블릿 객체를 생성하고 doGet() 메소드를 호출한 것은 무엇일까? 바로 서블릿 컨테이너이다.

서블릿 컨테이너는 다음과 같은 순서로 동작한다.

1. WEB-INF/web.xml 파일을 로딩하여 구동
   
2. 브라우저로부터 /hello.do 요청을 수신
   
3. hello.HelloServlet 클래스를 찾아 객체를 생성하고 doGet() 메소드 호출
   
4. doGet() 메소드 실행 효과를 클라이언트 브라우저로 전송

즉, 컨테이너는 자신이 관리할 클래스들이 등록된 XML 설정 파일을 로딩하여 구동하고, 클라이언트 요청이 들어오는 순간 XML 설정 파일을 참조하여 객체를 생성하고 객체의 생명주기를 관리한다. 기존의 자바 기반으로 개발할 때는 객체를 생성하고 객체 간 의존관계를 처리하는 것에 대한 책임은 개발자에 있었다. 하지만 제어의 역행은 객체의 생성과 객체들 사이의 의존관계를 컨테이너가 처리하는 것을 의미하며 결과적으로 낮은 결합도의 컴포넌트를 구현할 수 있게 한다.

---

아래 예제를 한 번 살펴보자. A TV와 B TV가 있고 이 두 TV의 기능은 이름만 다를 뿐 같다. 

```java
public class A_TV {
	public void powerOn() {
		System.out.println("A_TV -- 전원 on");
	}
	public void powerOff() {
		System.out.println("A_TV -- 전원 off");
	}
	public void volumeUp() {
		System.out.println("A_TV -- 볼륨 up");
	}
	public void volumeDown() {
		System.out.println("A_TV -- 볼륨 down");
	}
}
```

```java
public class B_TV {
	public void turnOn() {
		System.out.println("B_TV -- 전원 on");
	}
	public void turnOff() {
		System.out.println("B_TV -- 전원 off");
	}
	public void soundUp() {
		System.out.println("B_TV -- 볼륨 up");
	}
	public void soundDown() {
		System.out.println("B_TV -- 볼륨 down");
	}
}
```

```java
public class User {
	public static void main(String[] args) {
		A_TV a_TV = new A_TV();
		a_TV.powerOn();
		a_TV.volumeUp();
		a_TV.volumeDown();
		a_TV.powerOff();
	}
}
```
사용자가 만약 A TV를 사용하다가 B TV로 교체하려고 한다면, 코드는 아래와 같이 전체적으로 수정해야 한다. 만약 User와 같은 클라이언트 프로그램이 하나가 아니라 여러 개라면 유지보수는 물론 TV 교체는 어려워질 것이다.

```java
public class User {
	public static void main(String[] args) {
		B_TV b_TV = new B_TV();
		b_TV.turnOn();
		b_TV.soundUp();
		b_TV.soundDown();
		b_TV.turnOff();
	}
}
```

이와 같이 하나의 클래스가 다른 클래스와 많이 연결되어 있으면 '결합도가 높은 프로그램'이라고 표현하며, 결합도가 높은 프로그램은 유지보수가 어렵다는 단점이 있다. 결합도를 낮추기 위해서는 1) 다형성과 2) 디자인 패턴을 이용할 수 있다.

## '다형성'을 이용하여 결합도 낮추기

```java
public interface TV {
	public void powerOn();
	public void powerOff();
	public void volumeUp();
	public void volumeDown();
}
```

```java
public class A_TV implements TV {
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
public class B_TV implements TV {
	@Override
	public void powerOn() {
		System.out.println("B_TV -- 전원 on");
	}
	@Override
	public void powerOff() {
		System.out.println("B_TV -- 전원 off");
	}
	@Override
	public void volumeUp() {
		System.out.println("B_TV -- 볼륨 up");
	}
	@Override
	public void volumeDown() {
		System.out.println("B_TV -- 볼륨 down");
	}
}
```

```java
public class User {
	public static void main(String[] args) {
		TV tv = new A_TV();
		tv.powerOn();
		tv.volumeUp();
		tv.volumeDown();
		tv.powerOff();
	}
}
```

```java
public class User {
	public static void main(String[] args) {
		TV tv = new B_TV();
		tv.powerOn();
		tv.volumeUp();
		tv.volumeDown();
		tv.powerOff();
	}
}
```

TV라는 인터페이스를 이용함으로써 TV를 좀 더 쉽게 결합할 수 있었다. 하지만 이 방법 역시, 클라이언트의 소스를 수정해야 한다. 좀 더 간편한 방식으로 TV를 교체할 수 있는 Factory 패턴을 살펴본다.

## 디자인 패턴을 이용하여 결합도 낮추기

```java
public class BeanFactory {
	public Object getBean(String beanName) {
		if (beanName.equals("samsung") {
			return new SamsungTV();
		} else if (beanName.equals("lg")) {
			return new LgTV();
		}
		return null;
	}
}
```

```java
public class User {
	public static void main(String[] args) {
		BeanFactory factory = new BeanFactory();
		TV tv = (TV)factory.getBean(args[0]);
		tv.powerOn();
		tv.volumeUp();
		tv.volumeDown();
		tv.powerOff();
	}
}
```

결국 클라이언트는 소스를 수정하지 않고도 실행되는 객체를 변경할 수 있게 된다. 이러한 결과는 BeanFactory에서 TV 객체를 생성하여 리턴하기 때문이다.  User 클래스에서는 객체를 직접 생성하지 않고 객체가 필요하다는 것을 BeanFactory에 요청하기만 하면 BeanFactory에서는 클라이언트가 사용할 TV 객체를 적절히 생성하여 넘겨주게 된다.



# 참고
---
- 스프링 퀵 스타트