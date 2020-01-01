---
title: "텍트스 인코딩 컨버터 작성 후기"
date: "2014-04-21"
slug: reviewing-text-encoding-converter-development
description: ""
author: Justin-Yoo
tags:
- lean-method
- text-encoding-converter
fullscreen: false
cover: ""
---

얼마전 어찌어찌 해서 미드 [House of Cards](http://www.imdb.com/title/tt1856010/) 시즌 1, 2를 전부 감상할 수 있는 기회가 생겼다. 기쁜 마음에 동영상을 재생했으나, 플레이어가 자막 파일의 인코딩을 `UTF-8`만 지원하는 것이다. 옵션을 찾아보면 `EUC-KR` 내지는 `KS_C_5601_1987` 인코딩도 지원할 수도 있겠겠으나, 그걸 그때그때 찾아서 바꾸어주기는 하염없이 귀찮고, 또한, 파일들을 매번 하나하나 인코딩을 열어 바꾸어 주기도 귀찮고 해서 인코딩을 바꾸어주는 콘솔 앱을 그냥 만들었다!

- 깃헙 리포지토리: [Text Encoding Converter](https://github.com/aliencube/Text-Encoding-Converter)
- 직접 다운로드: [Text Encoding Converter 1.0.0.0](http://github.aliencube.org/Text-Encoding-Converter/downloads/TextEncodingConverter-1.0.0.0.zip)

구글링을 조금만 해보면 리눅스 계열에서는 iconv 인가 하는 걸로 하면 된다고 하는데, 윈도우용은 아니니 쓸모가 없고, 다른 분들이 이미 또 GUI 버전으로 훌륭하게 만들어 놓은 것들도 있고 해서 그걸 쓰면 좋겠다마는... 딱히 어렵지 않을 것 같아서, 또 요즘 회사 플젝에서 남용(?)하고 있는 병렬처리 기법도 한 번 써먹어 볼 겸 해서 만들어 봤는데, 이게 또 하다 보니 자꾸 일이 커져만 간다. #내가_하는게_다_그렇지

일단은 성공적으로 잘 돌아가지 싶고, 시간 내서 윈도우용 GUI 앱으로도 만들어 볼 생각이다. 게다가 요즘 [Xamarin Studio](https://xamarin.com/)가 기가 막히게 잘 만들어져 있다고도 하니, 이걸 이용해서 한 번 맥 데탑용으로도 포팅을 해볼까 하는 망상(!)도 한 번 가져 본다. 집에 맥 한 대 없는 맥 개발자라니! 하지만 울 집에서 사육중인 [@haruair](https://twitter.com/haruair)님의 맥북을 고문하다 보면 뭔가 방법이 생길 수도 있지 않을까 싶기도 하다.

이걸 하면서 느낀 점이라고 한다면 일을 쓸데없이 키운다. 그냥 ConsoleApp 플젝 하나 만들어서 실행파일 하나만 두면 될 것을 괜히 ConsoleApp 플젝, Service 플젝, ViewModel 플젝, UnitTest 플젝 등등으로 나눠서 복잡도가 커졌다. 같은 시기에 [#이상한모임](https://twitter.com/search?q=%23%EC%9D%B4%EC%83%81%ED%95%9C%EB%AA%A8%EC%9E%84) 사람들은 뭔가 대단한 걸 후다닥 하루도 안걸려서 만들던데, 난 괜히 막 복잡하게 하는 경향이 심해... 일단 돌아가게 만들고 찬찬히 리팩토링을 하는 것이 가장 빠른 릴리즈 방법인데, 하다가 보면 기왕 하는거 이쁘게 제대로 만들어야지~ 하면서 이래 된다는 거... 쩝.

야튼, 혹시나 이 블로그 들어오시는 분들 중에 저 앱 테스트 해보실 분? 피드백 환영!
