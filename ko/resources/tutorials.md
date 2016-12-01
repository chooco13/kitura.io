---
### TRANSLATION INSTRUCTIONS FOR THIS SECTION:
### TRANSLATE THE VALUE OF THE title ATTRIBUTE AND UPDATE THE VALUE OF THE lang ATTRIBUTE.
### DO NOT CHANGE ANY OTHER TEXT.
layout: page
title: Kitura 튜토리얼
menu: resources
lang: ko
redirect_from: "/resources/tutorial-todo.html"
### END HEADER BLOCK - BEGIN GENERAL TRANSLATION
---

<div class="titleBlock">
  <h1>튜토리얼</h1>
  <p>튜토리얼들을 통해 Kitura 를 어떻게 쓰는지 배워봅시다.</p>
</div>

## Routing and Requests

### [Parsing Requests](/{{ page.lang }}/resources/tutorials/parsingrequests.html)

쿼리와 URL 파라미터들을 파싱하는 법, 그리고 JSON 리퀘스트를 다루는 법에 대해 배워봅시다.

### [Special Types of Response Handlers](/{{ page.lang }}/resources/tutorials/responsehandlers.html)

복잡한 루트들을 다루기 위한 response 핸들러를 정의하는 법을 배워봅시다.

### [Writing Custom Paths](/{{ page.lang }}/resources/tutorials/pathsyntax.html)

파라미터와 정규식을 통한 매칭을 사용하여 원하는 경로에 루트를 정의하는 법에 대해 배워봅시다.

---

## Security

### [Adding Authentication with Kitura-Credentials](/{{ page.lang }}/resources/tutorials/credentials.html)

Facebook Oauth 인증을 추가하는 법에 대해 배워봅시다.

### [Adding Sessions with Kitura-Session](/{{ page.lang }}/resources/tutorials/sessions.html)

유저 정보를 세션 플러그인을 이용하여 저장하는 법에 대해 알아봅시다.

### [Enabling SSL/TLS on Kitura](/{{ page.lang }}/resources/tutorials/ssl.html)

보안 강화를 위해 SSL/TLS를 적용하는 법에 대해 알아봅시다.

---

## Other Topics

### [Using Templating Engines with Kitura](/{{ page.lang }}/resources/tutorials/templating.html)

이 튜토리얼은 Mustache 나 Stencil 같은 인기있는 탬플릿 엔진들을 Kitura 에서 어떻게 사용할지를 알려줍니다.

### [Using FastCGI with Kitura](/{{ page.lang }}/resources/tutorials/fastcgi.html) (Linux only)

Kitura 는 FastCGI 1.0 을 지원합니다. 또한 Nginx와 Apache에서 테스트 되었습니다
