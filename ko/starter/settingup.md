---
### TRANSLATION INSTRUCTIONS FOR THIS SECTION:
### TRANSLATE THE VALUE OF THE title ATTRIBUTE AND UPDATE THE VALUE OF THE lang ATTRIBUTE.
### DO NOT CHANGE ANY OTHER TEXT.
layout: page
title: 준비하기
menu: starter
lang: ko
redirect_from: "/starter/setting up.html"
### END HEADER BLOCK - BEGIN GENERAL TRANSLATION
---

<div class="titleBlock">
	<h1>준비하기</h1>
	<p>Kitura 는 macOS와 Linux에서 실행할 수 있습니다.
	<br>
	시작하기 위해서, 몇 가지 필수 항목을 설치해야 합니다.</p>
</div>

## macOS

<span class="arrow">&#8227;</span> [Xcode 8.1](https://developer.apple.com/download/) 을 다운로드하고 설치해주세요.

<hr>
## Ubuntu Linux

Kitura 는 Ubuntu 14.04 LTS, Ubuntu 15.10, 그리고 Ubuntu 16.04 LTS 환경에서 테스트되었습니다.

<span class="arrow">&#8227;</span> 다음의 리눅스 시스템 패키지를 설치해주세요:

```
$ sudo apt-get update
$ sudo apt-get install clang libicu-dev libcurl4-openssl-dev libssl-dev
```

<span class="arrow">&#8227;</span> [swift.org](https://swift.org/download/)에서 Swift 3.0.1 을 다운로드 해주세요.

<span class="arrow">&#8227;</span> `.tar.gz` 파일을 압축해제한 후, 해제한 경로가 포함되도록 `PATH` 환경 변수를 업데이트 해주세요:

```
$ export PATH=<path to uncompressed tar contents>/usr/bin:$PATH
```

<hr>
## 다음 단계

이제 첫번째 Kitura 어플리케이션을 만들 준비가 되었습니다. [시작하기](/{{ page.lang }}/starter/gettingstarted.html) 를 배워보세요.
