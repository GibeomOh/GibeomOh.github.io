---
layout: post
title: Apache와 Tomcat의 차이 
date: 2016-02-10
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
 
아파치 서버 설정
---
Apache와 Tomcat을 연동하기 위해서는 mod_jk와 proxy를 이용하는 방법이 있다.
Tomcat-Apache plugin인 mod_jk를 사용해서 Apach를 연동하는 법을 알아보자.
* Apache Tomcat Connector를 다운 받는다. (http://tomcat.apache.org/connectors-doc/)


        cd /etc/httpd/modules
        wget http://www.apache.org/dist/tomcat/tomcat-connectors/jk/binaries/linux/jk-1.2.28/i586/mod_jk-1.2.28-httpd-2.2.X.so
        ln -s mod_jk-1.2.28-httpd-2.2.X.so mod_jk.so

		
* <IfModule mod_jk.c> 태그 안에 JkMount을 통해 Apache 서버에서 Tomcat 서버로 요청을 전달할 수 있다.


        JkMount /*.do worker1
		JkMount /*.jsp worker1
		...
식으로 작성하면 아파치 서버로 들어오는 요청의 주소가 *.do나 *.jsp라면 톰캣으로 요청을 전달하게 된다.


톰캣 서버 설정
---
톰캣 서버 설정은 server.xml 파일에서 할 수 있다.
파일을 들여다보면 Connector를 볼 수 있는데, Connector는 요청을 받고 응답을 리턴하는 endpoint이다.
각 Connector는 요청을 처리하기 위해 연관된 Container에게 요청을 넘긴다.
그 밑을 보면 Engine이 있는데, Engine은 적절한 Host(virtual host)로 처리를 넘기는 entry point이다.
우리는 임의의 디렉토리에 웹 애플리케이션을 위치시키고 싶을 때  server.xml에서 설정 할 수 있지만 
자카르타에서 비추하는 방법이기 때문에 host-manager.xml, manager.xml 등의 파일을 저장해서 이름을 바꾸고
안에 내용중 docBase와 path를 바꾸하고 한다.
		<Context path="/myTest" docBase="C:\myTest" debug="0" privileged="true" reloadable="true">
		<Logger className="org.apache.catalina.logger.FileLogger" directory="logs"  prefix="localhost_log." suffix=".txt" timestamp="true"/>
		</Context>
- path : 웹어플리케이션의 경로명(http://localhost/'요기 붙을 내용')
- docBase : 웹어플리케이션이 위치한 폴더의 경로명(실제 경로)
정리하면, Context는 특별한 Viertual Host에서 작동하는 하나의 Web Application 이고
Web Application을 추가 하기 위해서는 <Host></Host> 사이에 <Context>를 추가하면 된다.
		

출처
---
[위키백과: 아파치 HTTP 서버](https://ko.wikipedia.org/wiki/%EC%95%84%ED%8C%8C%EC%B9%98_HTTP_%EC%84%9C%EB%B2%84)<br>
[OKKY: apache와 tomcat의 정확한 차이](http://okky.kr/article/196722)<br>
[위키백과: 아파치 톰캣](https://ko.wikipedia.org/wiki/%EC%95%84%ED%8C%8C%EC%B9%98_%ED%86%B0%EC%BA%A3)<br>
[Apache와 Tomcat의 역할](http://storyjava.tistory.com/96)<br>
[mod_jk 사용법](http://jkkang.net/java/mod_jk/mod_jk_install.html)<br>
[톰캣에 어플리케이션 추가하기!](http://blog.daum.net/_blog/BlogTypeView.do?blogid=090sk&vblogid=&beforePage=2&maxarticleno=5494233&minarticleno=5494233&maxregdt=20090101205621&minregdt=20090101205621&currentPage=1&listScale=20&viewKind=&dispkind=B2201&CATEGORYID=703968&categoryId=703968&articleno=&regdt=&date=&calv=&chgkey=FUOyxhxFyv5jAVvGlcs43Ji18l-4-pbKU2nYh4-pD950&totalcnt=5)<br>
