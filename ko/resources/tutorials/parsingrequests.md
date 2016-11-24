---
### TRANSLATION INSTRUCTIONS FOR THIS SECTION:
### TRANSLATE THE VALUE OF THE title ATTRIBUTE AND UPDATE THE VALUE OF THE lang ATTRIBUTE.
### DO NOT CHANGE ANY OTHER TEXT.
layout: page
title: Parsing Requests
menu: resources
lang: ko
redirect_from: "/resources/tutorial-todo.html"
### END HEADER BLOCK - BEGIN GENERAL TRANSLATION
---

<div class="titleBlock">
  <h1>Parsing requests</h1>
  <p>아래 예제들은 Kitura 를 통해 데이터들이 서로 다른 방식으로 파싱될 수 있다는 것을 보여줍니다.</p>
</div>

## Parsing URL Encoded Parameters

"`:`" 로 시작하는 경로명에 매칭되는 URL 파라미터를 명시할 수 있습니다. 뒤에 있는 name 은 파라미터 딕셔너리의 키입니다.

```swift
router.get("/name/:name") { request, response, _ in
    let name = request.parameters["name"] ?? ""
    try response.send("Hello \(name)").end()
}
```
이 예제는 `/name` 가 아닌 `/name/Bob`, `/name/Joe` 에 매칭될 것입니다.

---

## Parsing Query Parameters

`RouterRequest` 의 `queryParameters` 딕셔너리를 통해 쿼리 파라미터에 접근할 수 있습니다.

```swift
router.get("/name") { request, response, _ in
    let name = request.queryParameters["name"] ?? ""
    try response.send("Hello \(name)").end()
}
```

이 예제에서는, `/name?name=Dan` 이 입력으로 들어오게되면, 화면에 "Hello Dan" 라 출력될 것입니다.

---

## Parsing String Posts

post 리퀘스트들의 body 는 `readString` 메소드를 통해 string으로 받을 수 있습니다.

```swift
router.post("/name") { request, response, _ in
    let name = try request.readString() ?? ""
    try response.send("Hello \(name)").end()
}
```

---

## Parsing JSON Posts

내장된 body 파싱 미들웨어 를 통해 JSON을 포함한 다양한 body 타입들을 파싱할 수 있습니다.

<span class="arrow">&#8227;</span> `Package.swift` 파일에 SwiftyJSON 를 추가하고 파일 상단에도 `import SwiftyJSON` 를 추가하여 SwiftyJSON 를 임포트하세요

> ![tip] Tip: Kitura가 의존하고 있는 SwiftyJSON 버전과 동일한 버전을 import 하도록 해주세요. SwiftyJSON 버전은 `Packages/Kitura*/Package.swift` 를 살펴보면 찾을 수 있습니다.

<span class="arrow">&#8227;</span> body parser 가 `/name` 으로 시작되는 모든 경로에서 적용되도록 명시해주세요.

```swift
router.all("/name", middleware: BodyParser())
```

<span class="arrow">&#8227;</span> body property 로 부터 parsed body 를 얻기 원하는 경로를 명시해 주세요.

```swift
router.post("/name") { request, response, next in
    guard let parsedBody = request.body else {
        next()
        return
    }

    switch(parsedBody) {
    case .json(let jsonBody):
            let name = jsonBody["name"].string ?? ""
            try response.send("Hello \(name)").end()
    default:
        break
    }
    next()
}
```

[info]: ../../../assets/info-blue.png
[tip]: ../../../assets/lightbulb-yellow.png
[warning]: ../../../assets/warning-red.png
