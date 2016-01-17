---
layout: post
title: OAuth 정리
date: 2016-01-17
tags: OAuth
category: study
---

Summary
---
OAuth의 개념과 Facebook 연동 예제를 통해 간략하게 알아본다.  

OAuth 란?
---
OAuth는 사용자가 소유하고 있는 리소스에 제한된 액세스를 서드파티 클라이언트에게 부여할 수 
있도록 새롭게 등장한 웹 표준. 

OAuth는 사용자가 제한된 기능을 갖춘 토큰을 발행하여 애플리케이션과 데이터에 대한 제한된 액세스를 부여할 수 있음.

잠깐, JSON 이란?
---
JSON(JavaScript Object Notation)은 속성-값 쌍으로 이루어진 데이터 오브젝트를 전달하기 위해 
인간이 읽을 수 있는 텍스트를 사용하는 개방형 표준 포맷이다. 

비동기 브라우저/서버 통신 (AJAJ)을 위해, 넓게는 XML(AJAX가 사용)을 대체하는 주요 데이터 포맷이다. 

특히, 인터넷에서 자료를 주고 받을 때 그 자료를 표현하는 방법으로 알려져 있다. 
자료의 종류에 큰 제한은 없으며, 특히 컴퓨터 프로그램의 변수값을 표현하는 데 적합하다.

본래는 자바스크립트 언어로부터 파생되어 자바스크립트의 구문 형식을 따르지만 언어 독립형 데
이터 포맷이다. 

즉, 프로그래밍 언어나 플랫폼에 독립적이므로, 구문 분석 및 JSON 데이터 생성을 
위한 코드는 C, C++, C#, 자바, 자바스크립트, 펄, 파이썬 등 수많은 프로그래밍 언어에서 쉽게 
이용할 수 있다.

JSON은 두개의 구조를 기본으로 두고 있다:

* name/value 형태의 쌍으로 collection 타입. 다양한 언어들에서, 이는 object, record, 
struct(구조체), dictionary, hash table, 키가 있는 list, 또는 연상배열로서 실현 되었다.
* 값들의 순서화된 리스트. 대부분의 언어들에서, 이는 array, vector, list, 또는 sequence로서 
실현 되었다.

OAuth의 용어
---
Service Provider: 자원을 제공하는 웹서비스. 트위터 또는 페이스북 서비스를 의미.

Consumer: 서비스 프로바이더의 자원에 접근하는 서드파티 웹사이트/애플리케이션.

Protected Resource: 서비스 프로바이더가 보유한 데이터. 트윗글과 팔로워 목록 등과 같은 데이터
Consumer Key/Secret: 서비스 프로바이더는 자신들의 서비스에 서드파티들이 접근할 수 있도록 
하는데, 이때 각 서드파티들을 고유하게 식별하기 위한 값이 Consumer Key 이며, 그에 대한 확인을 
위한 값이 Consumer Secret 이다. (아이디/비밀번호와 유사)

Request Token: 액세스 토큰과 교환하기 위한 사용자의 승인이 떨어지지 않은 토큰. 토큰은 key와 
secret으로 구성.

Access Token: 사용자에 의해 승인된 토큰. 이 토큰을 소유하면 해당 사용자의 자원을 사용할 수 있다.

OAuth Parameter: OAuth 인증을 위해 필요한 파라미터 값. oauth_라는 접두어로 시작.

OAuth의 간략한 흐름
---
1. Service Provider가 제공하는 Request Token URL에 접속하여, Request Token을 요청하여 얻는다. 
이 값은 Access Token과 교환하기 위한 값이며, 아직은 사용자의 승인이 되지 않은 토큰 값이다.

2. Service Provider가 제공하는 Authorize URL에 접속하면서 Request Token 값을 전달하면, 
사용자의 인증페이지를 볼 수 있게 된다. 사용자가 (로그인을 하고) 접손 허용을 하면, Verifier 값을 
얻을 수 있게 된다.
(이 때, Consumer가 웹서비스 또는 애플리케이션인지에 따라 Verifier 값을 다르게 수신하게 된다.
웹서비스라면, Service Provider에게 제공한 callback 주소로 리다이렉트 되면서 Verifier가 
전달되며, 애플리케이션이면, 리다이렉션 없이 pincode를 발급해준다. 이 pincode를 추출하여 
Verifier로 사용한다.)

3. Service Provider가 제공하는 Access Token URL로 접속하여, Request Token과 Verifier를 함께 
전달하면 Access Token을 얻을 수 있게 된다.

4. 획득한 Access Token을 사용자의 계정에 따라 저장하여, 이후에 자원에 접근하기 위한 값으로 
사용할 수 있다.
![OAuth 흐름](http://cfile25.uf.tistory.com/original/176175494D1DB1A61BD40C)

페이스북 로그인 연동 OAuth 2.0
---
웹사이트를 참고하면서 로그인 연동을 시험해보자.

1. 먼저 페이스북에 앱을 만들고 로그인 할 수 있는 앱아이디와 시크릿 코드를 발급받는다.
[Facebook 개발자](https://developers.facebook.com/)

2. 앱을 적용할 사이트의 주소를 입력한다.

3. 만든 앱의 Settings에서 연락 이메일과 정보를 입력한다.

4. Status & Review 화면에서 
Do you want to make this app and all its live features available to the general public?
오른쪽 버튼을 YES로 설정한다.
만든 앱을 모든 사용자가 사용할 수 있게 배포하는 설정이다.

여기까지 진행했다면 우리가 만든 앱으로 페이스북 사용자가 로그인 할 수 있는 준비가 됬다.

1. 앱의 Dashboard 탭에서 Get Started with the Facebook SDK 를 통해 코드를 받을 수 있다.
Choose a flatform을 누르고 웹사이트를 클릭한다.

2. 자바 스크립트를 통한 로그인 구현

       window.fbAsyncInit = function() {
          FB.init({
             appId      : 'your-app-id',
             xfbml      : true,
             version    : 'v2.5'
          });
       };

       (function(d, s, id){
          var js, fjs = d.getElementsByTagName(s)[0];
          if (d.getElementById(id)) {return;}
          js = d.createElement(s); js.id = id;
          js.src = "//connect.facebook.net/en_US/sdk.js";
          fjs.parentNode.insertBefore(js, fjs);
       }(document, 'script', 'facebook-jssdk'));


   로그인 버튼을 눌렀을 때
 

       // Only works after `FB.init` is called
       function myFacebookLogin() {
          FB.login(function(){}, {scope: 'publish_actions'});
       }

       <button onclick="myFacebookLogin()">Login with Facebook</button>

       FB.login(function(){
          // Note: The call will only work if you accept the permission request
          FB.api('/me/feed', 'post', {message: 'Hello, world!'});
       }, {scope: 'publish_actions'});




출처
---
[개발자를 위한 Facebook](https://developers.facebook.com/docs/javascript/examples)<br>
[JSON 개요](http://www.json.org/json-ko.html)<br>
[위키백과 - JSON](https://ko.wikipedia.org/wiki/JSON)<br>
[페이스북 로그인 연동 OAuth 2.0 인증, 얍소프트의 야무진 블로그](http://blog.naver.com/yapsoft/220125205511)<br>
[OAuth의 개념과 대략적인 흐름, 로그의 노트](http://hiddenviewer.tistory.com/16)