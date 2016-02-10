---
layout: post
title: Apache와 Tomcat의 차이 
date: 2016-01-17
tags: Apache Tomcat
category: study
---

Summary
---
Apache와 Tomcat의 차이점을 알아본다.  

Apache란?
---
Apache Tomcat을 하나의 프로그램이라고 알고 있었지만, 
통상적으로 Tomcat 하나의 프로그램을 말한다. 
먼저, Apache는 HTTP 웹 서버를 말한다. 
프로토콜을 이해하고 클라이언트와의 통신을 담당하며 
웹 서버로 들어온 요청을 웹어플리케이션 서버로 넘겨주는 역할을 한다.

Tomcat이란?
---
Tomcat은 아파치 톰캣(Apache Tomcat)으로 불리며 
서블릿 컨테이너만 있는 웹 애플리케이션 서버를 말한다. 
즉 톰캣은 웹 서버(Apache)와 연동하여 자바 서버 페이지(JSP)와 
자바 서블릿이 실행할 수 있는 환경을 제공한다.

그럼 Apache와 Tomcat의 차이점은?
---
Apache는 웹 서버로 정적인 데이터를 처리하고
Tomcat은 웹 애플리케이션 서버로 동적인 데이터를 처리하는 서버이다.
즉, 이미지나 단순 HTML파일과 같은 리소스를 제공하는 서버는 웹 서버를 
통하면 WAS를 이용하는 것보다 안정적이다. 
하지만, DB와 연결되에 데이터를 주고 받고나 프로그램으로 데이터 조작이 필요한 경우에는
Tomcat과 같은 웹 애플리케이션 서버를 활용해야 한다. 
따라서, 성능향상을 위해선 Apache와 Tomcat을 설치해서 웹 서버의 역할과 WAS의 역할을
분리한다.
* Tomcat 5.5부터 Httpd의 native 모듈을 사용하기 때문에 동적인 모듈 뿐만 아니라
 정적 페이지 또한 처리가 가능하다고 한다. 그래서 성능상의 차이가 없다고 한다.
 

출처
---
[위키백과: 아파치 HTTP 서버](https://ko.wikipedia.org/wiki/%EC%95%84%ED%8C%8C%EC%B9%98_HTTP_%EC%84%9C%EB%B2%84)<br>
[OKKY: apache와 tomcat의 정확한 차이](http://okky.kr/article/196722)<br>
[위키백과: 아파치 톰캣](https://ko.wikipedia.org/wiki/%EC%95%84%ED%8C%8C%EC%B9%98_%ED%86%B0%EC%BA%A3)<br>
[Apache와 Tomcat의 역할](http://storyjava.tistory.com/96)<br>