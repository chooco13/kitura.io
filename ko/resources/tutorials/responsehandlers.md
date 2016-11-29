---
### TRANSLATION INSTRUCTIONS FOR THIS SECTION:
### TRANSLATE THE VALUE OF THE title ATTRIBUTE AND UPDATE THE VALUE OF THE lang ATTRIBUTE.
### DO NOT CHANGE ANY OTHER TEXT.
layout: page
title: Response Handlers
menu: resources
lang: ko
redirect_from: "/resources/tutorial-todo.html"
### END HEADER BLOCK - BEGIN GENERAL TRANSLATION
---

<div class="titleBlock">
	<h1>Response handlers</h1>
	<p>Kitura 는 복잡한 경로들도 표현할 수 있도록 다양한 방법의 핸들러를 제공하고 있습니다.</p>
</div>

## Multi-handlers

Response 들은 영역을 나눠서 로직에 따라 여러가지 핸들러를 거칠 수 있습니다.

```swift
router.get("foo", handler: { request, response, next in
    if request.queryParameters["bar"] == nil {
        response.error = NSError(domain: "RouterTestDomain", code: 1, userInfo: [:])
    }
    next()
}, { request, response, next in
    // Only gets called if no error
})
```

---

## Multi-HTTP Verbs

`route` 메소드를 이용하여 하나의 경로에 여러개의 HTTP verbs 를 설정할 수 있습니다.

```swift
router.route("foo")
.get() { request, response, next in
    // Get logic here
}
.post() { request, response, next in
    // Post logic here
}
```

---

## Sub-routers

복잡한 라우터들은 서브라우터들로 나눌 수 있습니다. 서브라우터들은 경로 접두어를 붙일 수 있습니다. 서브라우터들은 여러개의 나눠진 파일에 위치하게 할수도 있습니다.

```swift
let subrouter = Router()
subrouter.get("/") { _, response, _ in
    try response.send("Hello from subsection").end()
}

subrouter.get("/about") {_, response, _ in
    try response.send("About the subsection").end()
}

let mainRouter = Router()
mainRouter.get("/") {_, response, _ in
    try response.send("Welcome").end()
}
mainRouter.all("sub", middleware: subrouter)

// Add HTTP Server to listen on port 8090
Kitura.addHTTPServer(onPort: 8090, with: mainRouter)

// start the framework - the servers added until now will start listening
Kitura.run()
```
localhost:8090 에 GET request 를 하게되면 "Welcome" 을 반환할 것입니다. 그리고 localhost:8090/sub 에 GET request 를 하게 되면 "Hello from subsection" 를 반환할 것입니다.
