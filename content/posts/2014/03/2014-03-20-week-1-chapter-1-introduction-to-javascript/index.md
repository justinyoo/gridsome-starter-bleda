---
title: "Week 1: Chapter 1. Introduction to JavaScript"
date: "2014-03-20"
slug: week-1-chapter-1-introduction-to-javascript
description: ""
author: Justin-Yoo
tags:
- javascript
fullscreen: false
cover: ""
---

며칠전 [@n0lb00](https://twitter.com/n0lb00)님께서 제안하셨던 [자바스크립트 제대로 배우기](http://nolboo.github.io/blog/2014/03/13/how-to-learn-javascript-properly/)를 **제대로** 해보고자 [자바스크립트 스터디 모임](https://www.facebook.com/groups/learnjsproperly/)에 가입한 후 책도 [@haruair](https://twitter.com/haruair)님 도움으로 [아마존에서 구입](http://www.amazon.com/gp/product/0596805527)을 했다. 물건너오는 책이다보니 며칠 걸리길래 그냥 놀고 있으려고 했으나 온라인 맛보기 페이지가 존재하는지라 그냥 노는 김에 살짝 읽어보면서 요약을 할까 한다.

항상 하던 대로 불릿 포인트로 정말로 **요약**만 할 것이나 책을 읽어본 사람이라면 무슨 말인지는 다 알 거임. (정말?) 일단 1장 요약 들어감.

## 개요

- 자바스크립트는 웹 개발자라면 반드시 배워야 하는 삼대 기술 중 하나 – HTML은 웹 페이지의 컨텐츠를 구성하고, CSS은 웹 페이지의 모양을 결정하고, 자바스크립트는 웹 페이지의 행동방식을 결정한다.
- 자바와 자바스크립트의 차이점은 오스트리아와 오스트레일리아, 키위와 키위새의 차이만큼 차이가 있다. 자바스크립트는 오랜 시간동안 발전해서 이제는 단단하고 효과적인 프로그래밍 언어가 되었다. 가장 최근 버전에서는 대규모 소프트웨어 개발을 위한 새로운 기능들도 규정할 정도이다.
- 일반적인 프로그래밍 언어들이 기본적인 입력과 출력을 담당하는 API나 라이브러리를 갖는데 비해, 자바스크립트는 텍스트, 배열, 날짜, 정규표현식 등과 같은 것들을 다루는 최소한의 API만 갖고 정작 입출력 관련 기능은 포함하지 않았다. 입출력 기능이나 좀 더 복잡한 고급 기능들 – 네트워킹, 스토리지, 그래픽 등은 자바스크립트를 포함하는 **호스트 환경**(일반적으로 웹 브라우저)에서 다루게끔 한다.

## 자바스크립트 코어

- 자바스크립트는 다양한 밸류 타입을 지원하는데 몇가지 주목해야 할 부분은 다음과 같다.

```js
x = null;      // null은 값이 없다는 의미의 특수 값이다.
x = undefined  // undefined가 다른 언어에서의 null과 비슷한 기능을 한다.

```

- 자바스크립트에서 다루는 또다른 아주 중요한 두가지 타입이 있는데 바로 `object`와 `array`이다.

```js
// 자바스크립트에서 가장 중요한 다타 타입은 object이다.
// object는 name/value 페어의 콜렉션 혹은 스트링/밸류 매핑이다.
var book = {                  // object는 중괄호로 둘러싼다.
    topic: "JavaScript",      // topic 이라는 프로퍼티는 "JavaScript"라는 값을 갖는다.
    fat: true                 // fat 이라는 프로퍼티는 true 값을 갖는다.
};                            // 중괄호를 닫아서 object의 끝임을 알린다.

// 프로퍼티에 접근할 때에는 . 또는 []을 사용한다.
book.topic                    // = "JavaScript"
book["fat"]                   // = true
book.author = "Flanagan";     // 새로운 프로퍼티를 곧바로 값을 할당하는 방식으로 해서 만들 수 있다.
book.contents = {};           // {}는 프로퍼티가 없는 빈 object이다.

// 자바스크립트는 array도 지원한다.
var primes = [2, 3, 5, 7];    // 네 개의 값이 들어 있는 array. array는 대괄호로 구분한다.
primes[0]                     // = 2: array의 최초 엘리먼트.
primes.length                 // = 4: array 안에 들어있는 엘리먼트의 갯수.
primes[primes.length-1]       // = 7: array의 마지막 엘리먼트.
primes[4] = 9;                // 새 엘리먼트를 추가하기.
primes[4] = 11;               // 기존 엘리먼트의 값을 바꾸기.

var empty = [];               // []는 엘리먼트가 없는 빈 array이다.
empty.length                  // = 0

// array와 object는 다른 array와 object를 포함할 수 있다.
var points = [                // 두 개의 엘리먼트를 갖는 array.
    { x: 0, y: 0 },           // 각각의 엘리먼트는 object이다.
    { x: 1, y: 1 }
];

var data = {                  // 두 개의 프로퍼티를 갖는 object.
    trial1: [[1, 2], [3, 4]], // 각각의 프로퍼티는 array.
    trial2: [[2, 3], [4, 5]]  // 각각의 array에 있는 엘리먼트는 또다시 array.
};

```

- 몇가지 용어 설명: `expression`, `statement`, `function`, `method` 등
- 유념해야 할 것은 `function`과 `object`가 결합하면 `method`가 탄생한다는 것. 좀 더 정확하게는 `object`의 프로퍼티로 `function`을 할당한다면 그것을 `method`라 부른다.

```js
var points = {};
points.calc = function (x, y) {
    return x + y;
};
points.calc(10, 20);          // = 30

```

- 자바스크립트는 객체지향 언어이지만 다른 객체지향 언어들과는 사뭇 다르다. 간단한 예를 들어보자면

```js
// Pythagorean이라는 object를 초기화하기 위해 생성자 function을 정의한다.
function Pythagorean (x, y) {  // 생성자 function은 관례적으로 PascalCase로 함.
    this.adjacent = x;         // this 라는 키워드를 이용해서 Pythagorean object의 adjacent, opposite 프로퍼티에
    this.opposite = y;          // 각각 x, y 값을 할당함.
};                             // 리턴값은 필요 없음.

// new 키워드를 이용해 Pythagorean object를 생성한다. 초기값을 3과 4로 주었다.
var p = new Pythagorean (3, 4);

// Pythagorean object에 prototype이라는 object를 통해 method를 정의한다.
Pythagorean.prototype.hypotenus = function () {
    return Math.sqrt(this.adjacent * this.adjacent + this.opposite * this.opposite);
};

// 이제 대각선의 길이를 구한다.
p.hypotenus()                  // = 5

```

## 클라이언트에서 쓰이는 자바스크립트

- 자바스크립트는 웹 브라우저 안에서 `<script>` 태그로 감싸 사용할 수 있다.
- 자바스크립트는 HTML 엘리먼트들을 다룰 수 있다.
- 자바스크립트는 CSS 엘리먼트들을 다룰 수 있다.
- 자바스크립트는 웹 브라우저의 이벤트들을 다룰 수 있다.
- 예제 `1-1 자바스크립트 대출계산기`를 통해 다양한 자바스크립트 기법을 맛볼 수 있다. 주석 잘 달아뒀으니까 찬찬히 잘 읽어볼 것.
