---
title: "C# 코딩 가이드라인 깃헙 페이지 제작 후기"
date: "2014-06-06"
slug: reviewing-github-pages-for-csharp-coding-guidelines
description: ""
author: Justin-Yoo
tags:
- github-pages
- javascript
- unicode
- base64
fullscreen: false
cover: ""
---

예전에 깃헙에 C# 코딩 가이드라인 리포지토리를 하나 열어둔 것이 있다. [https://github.com/aliencube/CSharp-Coding-Guidelines](https://github.com/aliencube/CSharp-Coding-Guidelines) 이 리포지토리는 원래 원저작자인 [Dennis Doomen](http://dennisdoomen.net/)[1](#fn-144-1)에게 한국어 번역 허락을 맡고 난 후 번역 작업을 하다가 만든 것이다. 원본 문서는 MS워드. 워드 문서에서 번역작업을 하다 보니 뭔가 꽤 많이 불편했다. 물론 잘 쓰는 사람들한테는 그닥 문제가 없겠지만, 난 불편했음. 그래서 기왕 작업하는 거 마크다운으로 수정이 편하게끔 작업을 해놓고 나중에 한국어로 번역해야지 하고 냅뒀는데...

얼마전에 [깃헙 API를 이용해서 정적 웹 페이지 구현하기](http://blog.aliencube.org/ko/2014/05/01/creating-github-pages-using-github-apis/)라는 포스트도 올렸고 해서, 그걸 이용해서 한번 만들어보자고 뚝딱거리면서 만들었다. 그렇게 해서 만들어진 웹사이트는 바로...

[**http://cscg.aliencube.org**](http://cscg.aliencube.org/)

기본적으로 모든 문서는 마크다운 문법으로 정리해서 리포지토리에 저장되어 있으니, 깃헙 페이지에서는 그 마크다운 문서를 마스터 브랜치에서 불러다가 파싱해서 꽂아주기만 하면 되는 셈이어서 딱히 어려운 작업은 아니었다.

그런데, 문제는 깃헙 API가 반환하는 데이터는 Base64 인코딩 문자열인데, 이게 한글이라든가 하는 유니코드가 들어가 있을 경우 자바스크립트의 `btoa` 함수가 제대로 작동하지 않는다는 데 있다. 기본적으로 ASCII 코드를 변환하는 함수이기 때문이다. 그래서 찾아낸 것이 바로 [https://github.com/infowrap/base64](https://github.com/infowrap/base64)라는 자바스크립트 라이브러리. 아스키 코드 뿐만 아니라 유니코드도 제대로 변환이 가능하다. 이제 한국어 번역 문서가 들어오면 글자 깨짐 없이 바로 화면상에 구현 가능. #신난다

또한 자바스크립트 자체적으로 URL을 파싱하는 기능이 부족하기 때문에 그것을 지원하는 [https://github.com/allmarkedup/purl](https://github.com/allmarkedup/purl) 라이브러리도 이용하여 쿼리스트링을 자바스크립트 상에서 다뤘다.

마지막으로 쿠키를 다루기 위해 [https://github.com/carhartl/jquery-cookie](https://github.com/carhartl/jquery-cookie) 라이브러리도 참조를 했다.

사실 부트스트랩 바탕이다보니 jQuery 지원은 기본적으로 가능하고 거기에 몇가지 필요한 자바스크립트 라이브러리들을 추가해서 쓰니 굉장히 쉽게 만들 수 있었다.

이제 남은 일은 한국어 번역하는 것. 언제 시작해서 언제 끝낼 수 있으려나...

* * *

2. Dennis Doomen은 [Fluent Assertions](https://github.com/dennisdoomen/fluentassertions) 라는 BDD용 테스트 라이브러리를 배포하는 나름 이바닥 유명한 개발자이기도 하다. [↩](#fnref-144-1)
