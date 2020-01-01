---
title: "윈도우에서 MP3 파일 한글 태그 유니코드로 손쉽게 변경하기"
date: "2015-05-26"
slug: converting-encodings-for-mp3-tags-to-unicode-on-windows
description: ""
author: Justin-Yoo
tags:
- mp3
- encoding
fullscreen: false
cover: ""
---

본인이 직접 CD에서 추출한 음원이 아닌 어둠의 경로를 통해 구한 mp3 파일들을 보면 보통 한글 태그들이 깨져 있는 경우가 많다. 특히 한글 윈도우에서 작성한 태그들은 영문 윈도우에서는 인코딩 문제로 인해 글자가 다 깨져 보이는 문제가 있다. 맥이나 리눅스 쪽에서는 이를 손쉽게 해결해 주는 라이브러리나 앱들이 꽤 있는 모양이던데 유독 윈도우 환경에서는 찾기 힘들다. 하지만 여기 소개하는 [MP3Tag](http://mp3tag.de/)라는 이름의 앱을 이용하면 손쉽게 수많은 mp3 파일들을 마우스 클릭 한두번 만으로 한꺼번에 유니코드 인코딩으로 변경할 수 있다.

웹사이트는 아래와 같다.

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2015/05/mp3tag-01.png)

- [http://mp3tag.de](http://mp3tag.de) (독일어)
- [http://mp3tag.de/en/index.html](http://mp3tag.de/en/index.html) (영어)

이 앱은 도네이션 웨어이다. 무료로 사용 가능하고, 기능에 만족했다면 도네이션을 단 100원이라도 해 주도록 하자. :-) 다운로드 받은 앱을 설치한 후 실행시키면 아래와 같은 화면이 나타난다.

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2015/05/mp3tag-02.png)

물론 위의 화면은 최초 실행 후 원하는 mp3 파일들을 불러들인 화면이다. 위의 스크린샷에서도 볼 수 있다시피 노래 제목들의 글자가 다 깨져서 읽을 수가 없는 상황이다. 한글 윈도우에서는 mp3 파일들의 태그들을 모두 cp-949 한글 인코딩으로 저장하기 때문에 영문 윈도우 혹은 다른 언어권 윈도우에서는 읽을 수가 없게 된다. 이럴 때 아래의 그림과 같이 `Actions (Quick)` 메뉴를 선택한다.

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2015/05/mp3tag-03.png)

그렇게 하면 아래와 같이 액션 타입을 선택하는 옵션 화면이 나오게 되는데 여기서 `Convert Codepage` 옵션을 선택하도록 한다.

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2015/05/mp3tag-04.png)

그다음에는 실제로 어느 필드를 변환할 것인지에 대해 아래와 같이 물어본다. 여기서는 `Title` 필드를 `Koean - 한국어 (949)`로 선택한다.

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2015/05/mp3tag-05.png)

그 다음에는 선택한 모든 파일들이 원하는 인코딩으로 바뀌면서 한글을 읽을 수 있게 됐다.

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2015/05/mp3tag-06.png)

하지만 여전히 mp3 파일에 방금 변환했던 결과가 반영되는 것은 아니다. 아래와 같은 추가적인 옵션을 세팅한다면 모든 깨진 한국어 제목들이 더이상 깨지지 않고 나타난다.

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2015/05/mp3tag-07.png)

이렇게 옵션을 저장한 후 위의 맨 왼쪽에 있는 `저장` 버튼을 클릭하면 모든 작업은 끝이다. 이렇게 해서 변환시킨 mp3 파일들은 이제 멀쩡하게 보일 것이다. 참쉽죠?
