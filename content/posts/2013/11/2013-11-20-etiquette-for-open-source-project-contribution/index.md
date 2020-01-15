---
title: "오픈소스 개발 참여시 지켜야 할 에티켓"
date: "2013-11-20"
slug: etiquette-for-open-source-project-contribution
description: ""
author: Justin-Yoo
tags:
- translations
fullscreen: false
cover: ""
---

**알림**: 이 글은 [Open Source Contribution Etiquette](http://tirania.org/blog/archive/2010/Dec-31.html)을 한국어로 번역한 것입니다.

## 오픈소스 개발 참여시 지켜야 할 에티켓

[미구엘 데 이카자 Miguel de Icaza](http://tirania.org/blog): 2010년 12월 31일 작성

오픈소스 프로젝트에 새로운 기능을 추가하거나 버그를 고치는 상황에 맞닥뜨린 몇몇 개발자들은 종종 최초로 시도하는 행동이 그 프로젝트에 참여하는 사람들을 위해 "**좀 더 쉽게 해줄 수 있는**" 코드를 만들어 준다고 하는 잘못된 생각을 갖고 있는 듯 하다.

**좀 더 쉽게 해줄 수 있는**, 이 말은 보통 메소드, 필드, 속성, 지역변수 같은 것들의 이름을 바꾼다거나, 메소드, 클라스들을 리팩토링 한다거나, 코드를 분리해서 다른 파일로 저장한다거나, 또는 여러 코드 파일들을 하나로 합친다거나, 알파벳 순서로 혹은 기능상의 순서로 정리한다거나, 비슷한 기능들을 묶어놓는다거나, 헬퍼 메소드들을 처음 또는 나중에 배치한다거나 하는 것들의 일련의 조합을 의미한다. 들여쓰기 변경, 변수들의 정렬 혹은 파라미터의 변경 등과 같은 수많은 작은 변화들도 함께 말이다.

**하지만 이것은 오픈소스 프로젝트에 공헌하는 올바른 방법이 아니다.**

당신이 어떤 오픈소스 프로젝트에 버그를 고친다거나 혹은 새로운 기능을 추가한다거나 하는 등의 활동으로 공헌하고자 할 때, 당신은 기존의 코딩 스타일, 코딩 패턴들을 사용해야 하고, 주 관리자의 코드 정리 방식에 따라야 한다.

프로젝트 관리자는 오랫동안 당신이 그 프로젝트에 참여했던 기간보다도 훨씬 더 오랫동안 작업을 해 왔다. 심지어 당신이 다음 프로젝트로 떠나버릴 지라도 그 관리자는 여전히 계속 그 프로젝트를 관리할 것이다.

프로젝트 관리자에게 패치를 보낸다거나 당신이 고친 부분과 함께 여기저기 이름을 변경한다거나, 리팩토링을 한다거나, 변수명, 메소드명 등을 바꾼다거나, 파일을 분리한다거나, 레이아웃을 바꾸는 등의 풀 리퀘스트를 보낸다고 하는 것은 굳이 기여라고 할 것이 아니다. 그건 그저 관리자에게 있어 숙제 같은 것이다.

프로젝트 관리자는 당신의 버그 패치를 봐야 하고, 실제 개선 사항이 무엇인지 찾아내야 하는 등의 일들을 하느라 그들이 정작 다른 일을 해야 하는 데 써야 할 귀중한 시간들을 낭비하는 것이다. 이것은 종종 당신의 _기여 부분_에 대한 노력을 허사로 만들어 버리기도 한다.

만약 당신이 정말로 코드 리팩토링을 해야 한다면, 우선은 그러한 변경 사항을 프로젝트 관리자와 논의하고 그 변경 사항에 대한 정당성을 확보해라. 만약 관리자가 그러한 변화에 동의한다면, 당신은 버그 픽스로부터 독립적인 코드 리팩토링 내용과 변경사항을 보관해야 한다. 그렇게 함으로써 코드 리뷰는 한층 더 깔끔해진다.

이렇게 당신의 소스코드 포크를 보관하는 것은 일반적으로 당신의 노력이 헛된 것이라는 것을 확인하는 것처럼 보인다. 게다가 다른 사용자들을 도울 수도 없는 것처럼 보이기도 한다. 수많은 사람들이 그렇게 해 왔다. 수백명의 개발자가 각자 _난 더 잘할 수 있어_, _난 저런 똑같은 실수는 하지 말아야지_ 등과 같은 생각을 갖고 매년 오픈소스 프로젝트들에 공헌을 하기 위해 도전을 하고 있는 셈이다. 오픈소스 프로젝트에 18년 이상을 관여하면서 오로지 손에 꼽을 수 있을 만큼의 오픈소스 프로젝트들이 포크를 하고 살아남았던 것을 생각해 본다. 그런 수백건의 실패사례들에서 벗어나자. 결국 이상한 것은 좋은 것이 아니다.

결론을 짓자면, 원작자의 오리지날 코딩 스타일들 존중해주고, 변경사항들을 리팩토링하고 싶다면 프로젝트 관리자에세 반드시 물어보는 것이 좋다.