---
title: "ViewResolver 공부"
date: 2020-08-18 11:44:28 -0400
categories: spring
toc: true
---

# Viewresolver 설정

SPRING 컨트롤러는 뷰에 의존적이지 않다.

컨트롤러가 지정한 뷰 이름으로부터 응답 결과 화면을 생성하는 View 객체는 ViewResolver가 구한다. SPRING은 몇 가지 ViewResolver
구현 Class를 제공하고 있는데, 이중 주요 ViewResolver 구현 Class는 아래와 같다.


| 구현CLASS | 설명 |
|--------|--------|
|**InternalResourceViewResolver**|뷰 이름으로부터 JSP나 Tiles 연동을 위한 View 객체를 리턴한다|
|**VelocityViewResolver**|뷰 이름으로부터 Velocity 연동을 위한 View 객체를 리턴한다.|
|**VelocityLayoutViewResolver**|VelocityViewResolver와 동일한 기능을 제공하며, 추가로 Velocity의 레이아웃 기능을제공한다.|
|**BeanNameViewResolver**|뷰 이름과 동일한 이름을 갖는 빈 객체를 View 객체로 사용한다.|
|**ResourceBundleViewResolver**|뷰 이름과 View 객체간의 Mapping정보를 저장하기 위해 Resource 파일을 사용한다.|
|**XmlViewResolver**|뷰 이름과 View 객체간의 Mapping정보를 저장하기 위해 XML 파일을 사용한다.|

## InternalResourceViewResolver 설정
InternalResourceViewResolver Class는 JSP나 HTML 파일과 같이 WEB Application의 내부 Resource을 이용하여 뷰를 생성하는 AbstractUrlBasedView타입의 뷰 객체를 리턴한다. 기본적으로 사용하는 View Class는 InternalResourceView Class이다.
 InternalResourceViewResolver Class는 다음과 같이 설정한다.

 `<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver" 
		p:prefix="/WEB-INF/viewjsp" p:suffix=".jsp"> </bean>`

기본적으로 사용되는 InternalResourceView Class는 단순히 지정한 Resource 경로로(일반적으로 JSP) 요청을 전달한다. 만약, SPRING의 국제화 관련정보를 JSTL에서 사용하고 싶다면, 다음과 같이 JstlView Class를 viewClass 프로퍼티로 지정하면 된다.

`
		<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver" 
					p:viewClass="org.sprinframework.web.servlet.view.JstlView"
					p:prefix="/WEB-INF/viewjsp" p:suffix=".jsp"/> `