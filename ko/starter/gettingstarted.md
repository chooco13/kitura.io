---
### TRANSLATION INSTRUCTIONS FOR THIS SECTION:
### TRANSLATE THE VALUE OF THE title ATTRIBUTE AND UPDATE THE VALUE OF THE lang ATTRIBUTE.
### DO NOT CHANGE ANY OTHER TEXT.
layout: page
title: Kitura "Hello World" 예제
menu: starter
lang: ko
redirect_from: "/starter/helloworld.html"
### END HEADER BLOCK - BEGIN GENERAL TRANSLATION
---

<div class="titleBlock">
	<h1>시작하기</h1>
	<p>첫번째 Kitura 웹 어플리케이션을 만들어봅시다!</p>
</div>

<span class="arrow">&#8227;</span> 먼저, 새 프로젝트 디렉토리를 만들어주세요:

```
$ mkdir myFirstProject
```

---
<span class="arrow">&#8227;</span> 그 후, Swift Package Manager 를 통해 새 Swift 프로젝트를 만들어 주세요.

```
$ cd myFirstProject
$ swift package init --type executable
```

---
<span class="arrow">&#8227;</span> 그러면 `myFirstProject` 내부의 구조는 다음과 같이 될 것입니다:

<pre>
myFirstProject
├── Package.swift
├── Sources
│   └── main.swift
└── Tests
</pre>

> ![lightbulb] Swift Package Manager 에 대한 더 많은 정보를 원하시면, [swift.org](https://swift.org/package-manager) 를 방문해주세요.

---
<span class="arrow">&#8227;</span> `Package.swift` 에, Kitura 를 프로젝트 dependency에 추가해 주세요.

```swift
import PackageDescription

let package = Package(
    name: "myFirstProject",
    dependencies: [
        .Package(url: "https://github.com/IBM-Swift/Kitura.git", majorVersion: 1, minor: 1)
    ])
```

---
<span class="arrow">&#8227;</span> `Sources/main.swift` 에, 다음 코드를 추가해주세요.

```swift
import Kitura

// Create a new router
let router = Router()

// Handle HTTP GET requests to /
router.get("/") {
    request, response, next in
    response.send("Hello, World!")
    next()
}

// Add an HTTP server and connect it to the router
Kitura.addHTTPServer(onPort: 8090, with: router)

// Start the Kitura runloop (this call never returns)
Kitura.run()
```

---
<span class="arrow">&#8227;</span> 어플리케이션을 컴파일해주세요:

```
$ swift build
```

---
<span class="arrow">&#8227;</span> 이제 새 웹 어플리케이션을 실행해보세요:

```
$ .build/debug/myFirstProject
```
---
<span class="arrow">&#8227;</span> 브라우저로 [http://localhost:8090](http://localhost:8090) 에 들어가보세요


<hr>
## logging 추가하기 (optional)

 위 예제 코드에는 Kitura 가 콘솔에 띄워주는 로깅 메시지가 없었습니다. 발생하는 문제들을 진단하는것을 돕기위해 logger를 추가하고 싶을수도 있습니다.

---
<span class="arrow">&#8227;</span> `Package.swift` 에 HeliumLogger dependency 를 추가해주세요.

```swift
import PackageDescription

let package = Package(
    name: "myFirstProject",
    dependencies: [
        .Package(url: "https://github.com/IBM-Swift/Kitura.git", majorVersion: 1, minor: 1),
        .Package(url: "https://github.com/IBM-Swift/HeliumLogger.git", majorVersion: 1, minor: 1)
    ])
```
---
<span class="arrow">&#8227;</span> `Sources/main.swift` 에서 HeliumLogger 를 사용할 수 있게 수정해주세요.


```swift
import Kitura
import HeliumLogger

// Initialize HeliumLogger
HeliumLogger.use()

// Create a new router
let router = Router()

// Handle HTTP GET requests to /
router.get("/") {
    request, response, next in
    response.send("Hello, World!")
    next()
}

// Add an HTTP server and connect it to the router
Kitura.addHTTPServer(onPort: 8090, with: router)

// Start the Kitura runloop (this call never returns)
Kitura.run()
```
<hr>
## 다음 단계

[클라우드에 어플리케이션 배포하기](/{{ page.lang }}/starter/deploying.html) 를 배워보세요.


[lightbulb]: ../../assets/lightbulb-yellow.png
