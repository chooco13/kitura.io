---
### TRANSLATION INSTRUCTIONS FOR THIS SECTION:
### TRANSLATE THE VALUE OF THE title ATTRIBUTE AND UPDATE THE VALUE OF THE lang ATTRIBUTE.
### DO NOT CHANGE ANY OTHER TEXT.
layout: page
title: Writing Custom Paths
menu: resources
lang: ko
redirect_from: "/resources/tutorials/pathsyntax.html"
### END HEADER BLOCK - BEGIN GENERAL TRANSLATION
---

<div class="titleBlock">
	<h1>원하는 경로 작성하기</h1>
</div>

Kitura 서버의 미들웨어와 핸들러를 연결할 때, Kitura 의 경로 구문을 통해 경로를 원하는대로 설정할 수 있습니다. 이 가이드는 Kitura 앱과 route 핸들러를 알고있다고 가정합니다.

---

## Static Paths
가장 기본적인 경로인 정적 경로가 지원됩니다. 간단하게 미들웨어나 핸들러가 마운트 할 때 경로를 지정하세요. 다음과 같이 말이죠:

```swift
// handler example
app.get("/test") { req, res, next in
    try res.send("Hello world").end()
}
```

이 경우에, `/test` 경로는 `/test` 에만 연결됩니다.

---

## Paths with Parameter(s)
`Kitura` 는 object에 대한 CRUD 작업을 수행하는 작업을 위해 경로에 파라미터를 사용하는것을 지원합니다. 간단하게 파라미터에 `:` 를 붙이세요. 다음과 같이 말이죠:

```swift
app.get("/:id") { req, res, next in
    let id = req.parameters["id"] ?? ""
    try res.send("Hello world to user \(id)").end()
}
```
이 경우에, `/:id` 경로는 `/123` 뿐 아니라 `/abc` 에도 적용됩니다. `id` 파라미터의 값은 `req.parameters["id"]`로 접근 할 수 있습니다.

---

## Parameter Modifiers

### <span class="arrow">&#8227;</span> Zero or One
`?` 연산자를 이용하여 파라미터가 옵션이라는 것을 나타낼 수 있습니다. 다음과 같이 말이죠:

```swift
app.get("/:id?") { req, res, next in
    let id = req.parameters["id"] ?? ""
    try res.send("Hello world to user \(id)").end()
}
```

이 경우에, `/:id` 경로는 `/` 와 `/123` 모두에 적용됩니다.

### <span class="arrow">&#8227;</span> Zero or Many
`*` 연산자를 이용하면 0번 매치되는 것도, 또는 여러번 매치되는 것들도 나타낼 수 있습니다. 다음과 같이 말이죠:

```swift
app.get("/:id*") { req, res, next in
    let id = req.parameters["id"] ?? ""
    try res.send("Hello world to user \(id)").end()
}
```

이 경우에, `/:id*` 경로는 `/`, `/123`, 그리고 `/abc/def/ghi` 에 적용됩니다.

### <span class="arrow">&#8227;</span> One or Many
`+` 연산자를 이용하면 한 번 이상 매치되는 것을 나타낼 수 있습니다. 다음과 같이 말이죠:

```swift
app.get("/:id+") { req, res, next in
    let id = req.parameters["id"] ?? ""
    try res.send("Hello world to user \(id)").end()
}
```

이 경우에, `/:id+` 경로는 `123` 과 `/abc/def/ghi` 에는 적용되지만 `/`에는 적용되지 않습니다.

### <span class="arrow">&#8227;</span> Custom Matching
추가적으로 파라미터를 수정하기 위해서, 어떠한 종류의 URL 을 받기를 원하는지 나타내기 위해 정규식을 사용할 수 있습니다. 간단하게 정규식을 `()` 안에 넣고 변수명 뒤에 덧붙이세요. 다음과 같이 말이죠:

```swift
app.get("/:id(\\d+)") { req, res, next in
    let id = req.parameters["id"] ?? ""
    try res.send("Hello world to user \(id)").end()
}
```

이 경우에, `:id(\\d+)` 경로는 오직 숫자들만 적용됩니다; `123` 에는 적용되지만, `/` 이나 `/abc` 에는 적용되지 않습니다.

### <span class="arrow">&#8227;</span> Unnamed Parameters
변수명을 지정하지 않고도 원하는 매치를 사용할 수 있습니다. 다음과 같이 말이죠:

```swift
app.get("/(\\d+)") { req, res, next in
    let id = req.parameters["0"] ?? ""
    try res.send("Hello world to user \(id)").end()
}
```

이 경우에, `/(\\d+)` 경로는 `/123` 에는 적용되지만 `/` 나 `abc` 에는 적용되지 않습니다. 매치된 파라미터는 인덱스를 통해 사용할 수 있습니다; 이경우에, 첫번째로 변수가 없는 파라미터 이기 때문에, 인덱스는 `0` 입니다.
