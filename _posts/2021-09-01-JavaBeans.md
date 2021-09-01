---
title: "자바 빈(Java Bean)"
excerpt: "자바 빈에 대하여 알아본다."

categories:
  - JSP
tags:
  - [Java, JSP]

toc: true
toc_sticky: true

date: 2021-09-01
last_modified_at: 2021-09-01
---
# 0. 자바 빈(Java Bean)
```
🚩 자바 빈(Java Bean)은 자바로 작성된 소프트웨어 컴포넌트이다.
```
자바 빈은 JSP 페이지의 디자인 부분과 로직 부분을 분리하므로 복잡한 코드를 줄이고 코드를 재사용하여 프로그램의 효율을 높인다는 장점이 있다. 또한, 코드를 재사용하므로 코드 작성 시간은 단축되고, 이미 사용되던 코드이므로 안정성이 보장되며 유지보수가 쉽다.

# 1. 자바 빈의 설계 규약
자바 빈을 작성하기 위해서는 설계 규약을 따라야 한다.

**클래스**
- 클래스는 반드시 패키지화 되어야 한다. 즉, default package가 아닌 특정 패키지에 클래스가 존재해야 한다.

**멤버 변수, 프로퍼티(property)**
- 멤버 변수는 프로퍼티(property)라 부르며, 접근 지정자는 private으로 정의한다.
  
- 프로퍼티에 접근하기 위해서는 getter/setter 메소드를 이용한다.

**생성자**
- 생성자는 매개변수가 존재하지 않는 기본 생성자여야 한다.

**getter/setter 메소드**
- 프로퍼티마다 별도의 getter/setter 메소드가 존재해야 한다.

- 모든 JSP 페이지에서 접근할 수 있도록 접근 지정자는 public으로 정의한다.

- getter 메소드에는 매개변수가 없어야 하며, setter 메소드에는 반드시 하나 이상의 매개변수가 존재해야 한다.

- 프로퍼티 타입이 boolean인 경우 getXXX 대신 isXXX 메소드로 정의할 수 있다.

**자바 빈 형태**

```JAVA
package 패키지명;

[import 패키지명;]

public class BeanClassName [implements java.io.Serializable] {
	// 멤버 변수 = 프로퍼티(property)
	private String name;
	private boolean flag;

	// 기본 생성자
	public BeanClassName() { }

	// getter 메소드
	public String getName() {
		return name;
	}

	public boolean isFlag() {
		return flag;
	}

	// setter 메소드
	public void setName(String name) {
		this.name = name;
	}

	public void setFlag(boolean flag) {
		this.flag = flag;
	}
}
```

# 2. 자바 빈 관련 액션 태그

JSP 액션 태그는 클라이언트 혹은 서버에게 어떠한 작동을 하도록 명령을 내리는 태그이다.

### `<jsp:useBean>`
`<jsp:useBean>` 태그는 자바 객체를 생성하거나 기존에 만들어진 객체를 반환한다.
```JSP
<jsp:useBean class="패키지명.클래스명" id="자바빈_이름" scope="page | request | session | application" />
```
아래 자바 코드와 같은 역할을 한다고 볼 수 있다.
```JAVA
자바빈_클래스명 자바빈_이름 = new 자바빈_클래스명();
```

`id`: 자바 빈 객체 인스턴스를 식별하는 이름
- 대소문자 구별
  
- 한 번 생성된 빈이 소멸할 때까지 중복 사용 불가
  
- Java에서의 객체 참조변수와 동일한 역할

`class`: 자바 빈에서 사용할 클래스명

`scope`: 자바 빈 객체의 참조 범위로, default 값은 page이다.
- page(default): 현재 페이지의 범위에만 한정되며, 페이지 처리가 끝나면 유효하지 않다.
  
- request: request 생명주기와 같이 요청을 받고 요청처리를 완료하는 시점까지 유효하다.
  
- session: 세션의 생명주기와 같이 세션이 설정된 유효시간 동안 유효하다.
  
- application: 웹 사이트가 실행되는 동안 유효하다.

### `<jsp:setProperty>`

`<jsp:setProperty>` 태그는 자바 빈에 속성 값을 할당한다.
```JSP
<jsp:setProperty name="빈 이름" property="속성명" value="설정할 값" />
<jsp:setProperty name="빈 이름" property="속성명" param="매개변수명" />
```
`name`: \<jsp:useBean>태그에 선언된 자바 빈 객체 인스턴스의 이름

`property`: 값을 설정할 자바 빈 프로퍼티(property) 이름

- `*`로 설정 시 ServletRequest 안의 모든 인자들 중 자바 빈 속성과 데이터 타입이 일치하는 것을 찾아 각 속성들을 각 인자들의 값으로 설정한다.

`value`: 자바 빈 속성에 설정할 값

`param`: 클라이언트에서 전송된 파라미터 값, 즉 쿼리스트링에 작성된 값을 속성 값으로 할당

### `<jsp:getProperty>`
`<jsp:setProperty>` 태그는 자바 빈의 속성 값을 가져온다.
```JSP
<jsp:getProperty name="빈 이름" property="속성명" />
```
`name`: 속성 값을 가져올 자바 빈 인스턴스의 이름

`property`: 가져올 속성의 이름