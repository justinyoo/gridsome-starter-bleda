---
title: "Feed Schemata 개발 일지"
date: "2014-01-27"
slug: feed-schemata-behind-the-scene
description: ""
author: Justin-Yoo
tags:
- feed-schema
fullscreen: false
cover: ""
---

## 배경

아는 사람**만** 아는 [Weird Feird](https://github.com/aliencube/Weird-Feird) 피드 애그리게이터. 나름 열쒸미 작업중이긴 한데, 이것저것 벌여놓은 판이 많아서 천천히 작업중. 현재까지는 워드프레스용으로만 피드 뽑아오는 것들 완료. 그런데, 이 작업을 하다보니 필요한 것이 바로 XML 스키마였음. 워드프레스용을 우선적으로 작업하다보니 우선 RSS 피드에 대한 포맷 정의가 필요한데, 이게 문서화된 것은 [RSS Advisory Board](http://www.rssboard.org/rss-specification)에 있고, RSS 피드 포맷에 대한 유효성 검사기도 있으나, 정작 이 유효성 검사를 위한 XML 스키파 파일에 대한 정의를 눈을 씻고 찾아봐도 없네? 굳이 하나 찾은 것이 있다면 바로 [RSS 2.0 Schema](http://rss2schema.codeplex.com/)에서 있었음. 하지만 기본 RSS 2.0 스펙에 대한 스키마만 존재할 뿐, 이것의 확장 스키마는 정말정말 못 찾겠더라. 어쩔 수 있나? 없으면 만들어야지. 그래서 만든 것이 바로 [Feed Schemata](https://github.com/aliencube/Feed-Schemata). ㅋ 각종 피드 포맷들에 대한 XML 스키마를 총체적으로 제공하는 리포지토리!

## RSS 1.0 과 2.0 의 차이?

[RSS Advisory Board](http://www.rssboard.org/rss-specification)에 가서 보니 신기하게도 RSS 버전이 0.92 에서 곧바로 2.0으로 뛰었다. 응? 그렇다면 1.0 버전은 없는 거싱가? 하고 찾아 봤는데, 아무렴 있지. 있고 말고. 근데, RSS 약어에 대한 정의가 다르더구만. 우리가 흔히 알고 있는 RSS는 `Really Simple Syndication`의 약자이고, RSS 1.0 포맷에 쓰인 것은 `RDF Site Summary`의 약자였음. 아무래도 이렇게 차이가 있다보니 버전 충돌을 피하기 위해 0.92에서 2.0으로 바로 뛴 것이고, RSS 1.0은 그상태에서 별도의 버전업 없이 머물러 있는 듯. 더 자세한 배경은 아무래도 그 둘이 통합이 되는 와중에 거의 RSS 1.0 포맷은 버려진 듯 싶더구만.

## 워드프레스 RSS

우선적으로 가장 널리 쓰이는 블로그 툴이 워드프레스이고, 그 워드프레스에서는 RSS 포맷을 지원하니까 그것부터 들여다 봤다. RSS 2.0 스펙의 가장 큰 문제점이라면 문제점인 것이 전문을 제공하지 않고 요약문만 제공한다는 것이다. 따라서, 전문을 제공하고자 하면 확장 스키마를 함께 제공해야 하는데, 이것은 [RSS 1.0의 Content 모듈](http://purl.org/rss/1.0/modules/content/)에서 제공한다. 이 외에도 몇가지 확장 모듈들이 있는데 워드프레스 RSS에서 추가로 제공하는 확장 스키마는 총 다섯가지.

- `xmlns:content="http://purl.org/rss/1.0/modules/content/"`
- `xmlns:wfw="http://wellformedweb.org/CommentAPI/"`
- `xmlns:dc="http://purl.org/dc/elements/1.1/"`
- `xmlns:atom="http://www.w3.org/2005/Atom"`
- `xmlns:sy="http://purl.org/rss/1.0/modules/syndication/"`
- `xmlns:slash="http://purl.org/rss/1.0/modules/slash/"`

## 확장 스키마는 도대체 몇개나 될까?

이 밖에도 구글링을 해보니 RSS 스펙을 확장시켜주는 추가 스키마들은 총 68가지나 된다!

https://twitter.com/justinchronicle/status/420932812519129091

그래서, 이걸 혼자 한번에 다 하는 건 불가능하고, 천천히 시간을 두고 추가시켜나갈 듯. 근데, 이런 거에 관심 있는 사람들이 있기는 할까? ㅡㅡ?
