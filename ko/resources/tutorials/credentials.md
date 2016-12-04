---
### TRANSLATION INSTRUCTIONS FOR THIS SECTION:
### TRANSLATE THE VALUE OF THE title ATTRIBUTE AND UPDATE THE VALUE OF THE lang ATTRIBUTE.
### DO NOT CHANGE ANY OTHER TEXT.
layout: page
title: Credentials
menu: resources
lang: ko
redirect_from: "/resources/tutorial-todo.html"
### END HEADER BLOCK - BEGIN GENERAL TRANSLATION
---

<div class="titleBlock">
	<h1>Kitura-Credentials</h1>
	<p><a href="https://github.com/IBM-Swift/Kitura-Credentials">Kitura-Credentials</a> 를 통해서 Kitura 앱에 사용자 인증을 추가 할 수 있습니다.<br>기존에 있는 인증 플러그인을 사용하거나, 또는 직접 만들어서 사용 할 수 있습니다.</p>
</div>

## 사용자 인증을 위해 Kitura-Credentials 를 설정하는 법

<span class="arrow">&#8227;</span> 앱에 Kitura-Credentials 를 통합하기 위해서, 먼저 Kitura 를 설정하세요:  

```swift
import Kitura

let router = Router()
```

<span class="arrow">&#8227;</span> 그 다음, 인증 프레임워크를 인스턴스를 생성 해주세요:

```swift
import Credentials

let credentials = Credentials()
```

<span class="arrow">&#8227;</span> 그 후, 사용하고 싶은 인증 플러그인을 설정하고 인증 프레임워크에 등록해주세요. 아래의 예제는 웹기반 페이스북 로그인 을 위한 인증 플러그인을 설정합니다. 가능한 인증 플러그인 목록은 [여기](https://github.com/IBM-Swift/Kitura-Credentials#list-of-plugins)에서 찾아보실 수 있습니다.

---

## 페이스북 로그인 예제
[Kitura-CredentialsFacebook](https://github.com/IBM-Swift/Kitura-CredentialsFacebook) 플러그인은 웹 기반 방식과 토큰 플로우 방식의 페이스북 로그인을 모두 지원합니다. 이 가이드는 페이스북에 앱을 등록하였고 페이스북을 통한 로그인 기능을 활성화시켰고 페이스북을 통해 웹 기반 OAuth 방식으로 사용자를 인증시키려 시도한다고 가정하고 진행됩니다.

<span class="arrow">&#8227;</span>  Kitura-CredentialsFacebook 를 웹 기반 방식으로 사용하려면, 먼저 세션을 설정해야 합니다:

```swift
// previous steps omitted for brevity

import KituraSession

// using in-memory session in this example; can also use other session stores
let session = Session(secret: "session_secret")

// configure Kitura router to use session
router.all(middleware: session)
```

<span class="arrow">&#8227;</span> 그 후, 플러그인을 설정해주세요:

```swift
import CredentialsFacebook

let fbCredentials = CredentialsFacebook(clientId: "<your-app-id>", clientSecret: "<your-app-secret>", callbackUrl: “<your-app-domain>/login/facebook/callback”)
```

<span class="arrow">&#8227;</span> 다음, 플러그인을 인증 프레임워크에 등록해주세요:

```swift
credentials.register(plugin: fbCredentials)
```

<span class="arrow">&#8227;</span> 마지막으로, 사용자 인증을 처리하기 위한 endpoints 를 서버에 설정해줍니다:

```swift
// Endpoint for starting the OAuth login flow
router.get(“/login/facebook”, handler: credentials.authenticate(credentialsType: fbCredentials.name)

// Endpoint for Facebook callback; handles exchange of temporary code for access token
router.get(“/login/facebook/callback”, handler: credentials.authenticate(credentialsType: fbCredentials.name))
```

이 endpoint 들을 통해, 로그인 프로세스를 시작하기 위해 사용자를 `/login/facebook` 로 리다이렉트 시킬 수 있습니다.

> ![lightbulb] 콜백 주소에 리다이렉트가 되게 하기 위해서는 페이스북 앱 설정에서 `<your-app-domain>/login/facebook/callback` 가 반드시 화이트리스트(whitelist)에 등록되어 있어야 합니다.  

지금까지의 과정이 웹 기반 페이스북 로그인을 위한 기본적인 설정입니다. 더 많은 사용법과 설정법은 Kitura-CredentialsFacebook 에서 참고해주세요.


[lightbulb]: ../../../assets/lightbulb-yellow.png
