---
title: "GitHub API Cache 개발 후기"
date: "2014-07-05"
slug: reviewing-github-api-cache-service-development
description: ""
author: Justin-Yoo
tags:
- restful-web-service
- web-api
- github
- cache
- rawgit
- appharbor
fullscreen: true
cover: https://sa0blogs.blob.core.windows.net/justinchronicles/2014/07/review.jpg
---

## 시작

늘상 그렇듯 시작은 참 단순했다. 한달쯤 전에 [WWDC](https://developer.apple.com/wwdc/)가 열렸고, 거기서 [Swift](https://developer.apple.com/swift/)라 불리는 새로운 개발언어를 공개했다. 아직까지 애플과 관계를 맺은 것이라곤 아이폰과 아이패드가 전부인지라 딱히 관심은 없었는데, 새로운 개발언어가 나왔고, 마침 또 [@jjuakim](https://twitter.com/jjuakim)님을 비롯한 몇몇 분이 번역을 시작하려고 하길래 숟가락을 놓자는 심정으로 같이 번역을 시작했다. 그렇게 번역이 끝나고 나서 이걸 웹으로 퍼블리싱을 하려니, 기존 번역문서가 모두 마크다운으로 작성되어 있었고, 깃헙에서 퍼블리싱을 하려고 하는 것이다. 그래서, 간단하게 [깃헙 페이지](https://pages.github.com/)를 이용하여 웹사이트를 퍼블리싱할 계획을 세웠다.

모든 것은 순조로왔다. 하지만, 실제로 웹사이트를 오픈한 날 오픈한지 5분도 안되어 사이트가 뻗었다. 정확하게는 사이트 개발시 사용한 깃헙 API 사용량이 초과된 것. 시간당 5000번의 API를 요청할 수 있는데, 사람들이 순식간에 몰리다 보니 이 오천번의 횟수 제한은 턱없이 부족한 것이었다. 그러는 와중에 [@golbin](https://twitter.com/golbin)님이 캐시 데이타를 사용하는 것이 어떤가 하는 것을 제안하셨다. [1](#fn-159-1)

눈이 번쩍 띄었다. 캐시 데이타만 쓸 수 있다면 굳이 API 리퀘스트를 날리지 않아도 되니까 말이다. 그래서 추천 받은 대로 [rawgit.com](http://rawgit.com) 서비스를 이용하는 것으로 바뀌었다. 그런데, 여기서도 문제가 있다. 가장 최근에 업데이트된 컨텐츠를 받으려면 커밋별 SHA 키값을 알아야 하는데, 이건 결국 깃헙에 리퀘스트를 날려 해결할 수 밖에 없는 것이다. 그러면서 생각해 낸 방법이 그렇다면 별도의 서비스를 이용해서 이 최신 SHA 값만 알아내면 이 값을 바탕으로 [rawgit.com](http://rawgit.com) 에서 캐시 결과를 끌어올 수 있다는 사실을 발견하고, 이 최근 SHA 값을 캐싱해주는 서비스를 만들기 시작했다. 이것이 바로 이 프로젝트의 시작이었다.

## 개발

나야 닷넷 개발자니까 당연하게(!) [ASP.NET Web API](http://www.asp.net/web-api)를 이용해서 만들어 보자고 생각하고 작업을 시작했다. 웹 API는 정말로 개발도 간단하고 사용법도 쉽기 때문에 실제로 쉽게 개발을 완료할 수 있었다. 개발 관련 소스코드 리포지토리는 [https://github.com/aliencube/GitHub-API-Cache](https://github.com/aliencube/GitHub-API-Cache)에서 확인해 볼 수 있다. 문제는 개발 이후 실제 서비스에 대한 내용이었다.

## 설치 및 운영

개발까지는 잘 됐다. 로컬에서 돌려서 잘 되는 것까지 확인이 다 끝났으니까. 문제는 이걸 도대체 어디에 설치해서 운영을 시작해야 하는 건지... 무료 호스팅 서비스를 찾아봤으나 닷넷 어플리케이션을 돌리기에는 한계가 있었다. [AWS](http://aws.amazon.com)에서 제공하는 마이크로 티어도 생각해 봤지만, 그건 처음 세팅하는 것 자체가 손이 너무 많이 가고, [Azure](http://azure.microsoft.com)로 돌리기에는 오버킬 같고... 등등 여러가지 고민을 하다가 한 3년쯤 전에 지인이 [AppHarbor](http://appharbor.com)라는 서비스를 추천해 준 것이 문득 생각났다. 그 당시에는 "클라우드가 뭐임? 먹는 거임? 우걱우걱?" 정도의 얕은 지식만을 갖고 있던 꼬꼬마 개발자였는지라 도대체 이 서비스가 뭘 하려고 하는 건지 알 수가 없었다. 게다가 "Git은 또 뭐여? SVN하고 뭐가 달라?" 하던 흑역사의 시절이었는지라... [#부끄럽다](https://twitter.com/search?q=부끄럽다)

어찌됐든, [Azure](http://azure.microsoft.com)에서도 비슷한 기능을 제공하고 있기 때문에 지난번에 참가했던 [Azure Bootcamp](http://global.windowsazurebootcamp.com)에서 봤던 기억을 되살려보니 아주 쉽게 쓸 수 있는 서비스였던 것이다. 그래서, 바로 계정을 만들고 퍼블리싱 작업을 시작했다. 데이터베이스 연동 없이 사이트 하나만 돌릴 경우에는 무료라는 것이 아주 매력적인 [AppHarbor](http://appharbor.com) 되겠다. [AppHarbor](http://appharbor.com)의 장점이라면 [GitHub](http://github.com), [BitBucket](http://bitbucket.org), [CodePlex](http://codeplex.com) 등과 같은 무료 소스코드 리포지토리에 연동을 시켜놓기만 하면 특정 브랜치로 푸시가 갈 경우 자동으로 다운 받아서 빌드한 후 테스트 케이스가 있으면 모든 테스트를 끝내고 퍼블리싱까지 자동으로 해준다는 것. 이 어찌 편리하지 않을쏘냐. 게다가 지금 퍼블리싱하려는 것은 굳이 데이터베이스 연동도 필요없으니, 아주 이상적이라 할 수 있다. 물론 자체 도메인이 아닌 `***.apphb.com` 스타일의 도메인을 써야한다는 제약이 있긴 하지만, 무료 서비스에 그정도 쯤은 괜찮다 할 수 있겠다. 그렇게 해서 서비스를 시작한 것이 바로

[**https://githubapicache.apphb.com**](https://githubapicache.apphb.com)

아직까지는 브랜치의 헤드가 가리키는 레퍼런스 값만을 호출하는 API만 존재하지만, 곧 모든 GitHub API들을 캐시할 수 있을 것이다.

## 결론

- 웹 API는 개발하기가 정말 편리하다. RESTful API 서비스를 고려중이라면 적극 추천.
- [AppHarbor](http://appharbor.com) 쓰세요, 두 번 쓰세요(...)
- 이걸 개발하던 덕분에 웹 API의 여러 가지 몰랐던 기능들을 알 수 있는 계기가 됐다. 도움을 주셨던 [@styletigger](https://twitter.com/styletigger) 님께 감사.

## 추가

내부적으로 쓸 API 서버는 여러번 만들어 봤지만, 누구나 접근 가능한 공개 API를 만들어 본 것은 이번이 처음이었다. RESTful API를 소비하는데 있어서 [jQuery](http://jquery.com) 또는 [AngularJS](http://angularjs.org) 등과 같은 자바스크립트 프레임워크를 통해 AJAX 리퀘스트를 보낼 경우 [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)를 서버측에서 고려해야 한다는 것을 전혀 생각도 하지 않고 있다가 굉장히 낭패를 겪었다. 다행히도 [NuGet](http://www.nuget.org)에서 Web API를 지원하는 [JSONP](http://www.nuget.org/packages/WebApiContrib.Formatting.Jsonp/) 라이브러리와 [CORS](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) 라이브러리가 있어서 그 둘을 이용해서 손쉽게 작업을 할 수 있었다. 덕분에 많은 것들을 다시금 배울 수 있는 계기가 되었다.

* * *

2. [내용이 업데이트 되었을 경우 퍼블리싱에 적용되지 않는 문제](https://github.com/lean-tra/Swift-Korean/issues/9) [↩](#fnref-159-1)
