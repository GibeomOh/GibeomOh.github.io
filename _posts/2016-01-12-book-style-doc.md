---
layout: post
title: Facebook Like Button for the Web
date: 2016-01-12
tags: facebook
category: tech
---

Step-by-Step
------------
1. Choose URL or Page
Pick the URL of a website or Facebook Page you want to use with the like button.

2. Code Configurator
Paste the URL to the [code configurator][url-1] and adjust settings like the `width` of your like button. Click the `Get Code` button to generate your like button code.

3. Copy & Paste HTML snippet
Copy and past the snippet into the HTML of the destination website.

Full Code Example
----------------
Copy & paste the code example to your website. Adjust the value `data-href` to your website URL. Next use the `og:***` meta tags to adjust your link preview. `og:url` and `data-href` should use the same URL.

	<!-- Load Facebook SDK for JavaScript -->
	<div id="fb-root"></div>
	<script>(function(d, s, id) {
	  var js, fjs = d.getElementsByTagName(s)[0];
	  if (d.getElementById(id)) return;
	  js = d.createElement(s); js.id = id;
	  js.src = "//connect.facebook.net/en_US/sdk.js#xfbml=1";
	  fjs.parentNode.insertBefore(js, fjs);
	}(document, 'script', 'facebook-jssdk'));</script>

	<!-- Your like button code -->
	<div class="fb-like" 
		data-href="http://www.your-domain.com/your-page.html" 
		data-layout="standard" 
		data-action="like" 
		data-show-faces="true">
	</div>

[url-1]:https://developers.facebook.com/docs/plugins/like-button#configurato