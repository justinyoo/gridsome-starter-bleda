---
title: "여러 개의 워드프레스 사이트들을 하나의 Azure Web App 인스턴스로 이전하기"
date: "2015-04-03"
slug: migrating-multiple-wordpress-sites-to-one-microsoft-azure-web-app
description: ""
author: Justin-Yoo
tags:
- wordpress
- migration
- azure
- webapp
fullscreen: true
cover: https://sa0blogs.blob.core.windows.net/justinchronicles/2015/04/wordpress-migration.jpg
---

## 삽질의 시작

현재 활발히(?) 운영하고 있는 블로그가 총 세 개가 있다.

- [Just In Chronicles](http://justinchronicles.net)
- [Aliencube Community](http://blog.aliencube.org)
- [DevKimchi](http://devkimchi.com)

이들 중에서 위 두개는 [GoDaddy](http://godaddy.com)에서 도메인을 구입한 덕분에 무료로 주는 호스팅 서비스에서 돌고 있었고, [DevKimchi](http://devkimchi.com)만 [Microsoft Azure](http://azure.microsoft.com) 기반으로 운영을 시작했다. 하지만 최근에 [Azure Web App](http://azure.microsoft.com/en-us/services/app-service/web/)으로 통합하고자 하는 의욕이 불끈 솟아 올랐다. 이유는 GoDaddy에서 받는 무료 호스팅 서비스가 너무 불안정해서 수시로 사이트가 뻗는 것이 가장 컸다고 할 수 있겠다. 그래서, 우선 GoDaddy에서 호스팅 받고 있는 두 사이트만 옮기고 나머지 하나는 나중에 통합하는 것이 계획의 시초.

## 삽질 시나리오

웹사이트 이전을 위한 시나리오는 아래와 같았다.

- 고대디 호스팅 워드프레스를 하나의 Azure Web App 아래로 이전
- 기존 URL은 그대로 유지한 채 서브 디렉토리에서 각각 운영
- 모든 첨부 파일은 [Azure Blob Storage](http://azure.microsoft.com/en-us/documentation/services/storage/)에 저장

모든 사이트를 [워드프레스](http://wordpress.org)로 운영을 하고 있다보니, [멀티 사이트](http://codex.wordpress.org/Create_A_Network)로 구성하는 것도 하나의 대안이었으나, 향후 각각의 사이트를 다시 분리해서 운영할 수도 있기 때문에 우선은 고려대상에서 제외하고, 각각의 사이트를 서브 디렉토리로 옮겨놓은 후 원래의 URL을 유지시키는 방향으로 시나리오를 결정했다. 또한, Web App 자체에 첨부 파일을 저장하기 보다는 Blob Storage를 이용하여 모든 이미지 파일들을 저장하기로 했다.

## 삽질 순서

### **1. Azure Web App 인스턴스 생성**

운이 좋게도 올해 [Microsoft MVP 수상](http://justinchronicles.net/ko/2015/04/02/became-a-microsoft-mvp/)의 부상으로 Azure 크레딧을 받을 수 있어서 그걸 이용하여 Azure Web App 인스턴스를 하나 만들었다. 데이터 센터는 Australia Southeast 지역으로 결정했는데, 아무래도 거주 지역이 호주 멜버른이다보니 최적의 선택이 아니었나 싶다. 이렇게 생성한 Web App 인스턴스에 커스텀 도메인을 연결하는 것은 [이 페이지](http://azure.microsoft.com/en-us/documentation/articles/web-sites-custom-domain-name)를 참고했다.

### **2. ClearDB 인스턴스 생성**

워드프레스는 [MySQL](http://mysql.com) 데이터베이스를 이용하는데, 이것을 클라우드 기반으로 포팅한 것이 [ClearDB](http://cleardb.com)이다. 이것은 써드파티 애플리케이션이므로 별도로 생성해야 하고, Azure Web App에서는 이 데이터베이스 링크를 사용한다.

### **3. Azure Blob Storage 인스턴스 생성**

앞서 시나리오에서 언급한 바와 같이, Blob 스토리지를 이용하여 모든 첨부 이미지들을 관리할 계획이므로 Blob Storage 인스턴스를 생성했다. Azure Web App과 달리 Blob Storage에는 커스텀 도메인을 하나만 연결 시킬 수 있다. 이부분이 조금 애매했음. 여러 사이트에서 하나의 스토리지에 접속을 하니까 기왕이면 여러 도메인을 연결할 수 있으면 좋겠구만.

### **4. 기존 데이터 및 웹사이트 백업**

GoDaddy 호스팅 사이트로 접속해서 데이터베이스와 웹사이트 파일들을 통째로 백업 받았다.

여기까지는 아무 문제 없이 진행됐던 상황. 이제 이 다음부터가 삽질에 삽질을 거듭하는 상황이 됐다.

### **5. `justinchronicles.net` 사이트 복원**

일단 백업 받은 첨부 파일들을 모두 Auzre Blob Storage로 옮기는 작업을 했다. 이것은 [Blob Transfer Utility](https://blobtransferutility.codeplex.com/)라는 앱을 이용했다. 굉장히 직관적인 사용법을 갖고 있지만, 이미지 파일의 확장자에 따라 [MIME type](http://en.wikipedia.org/wiki/Internet_media_type)을 수동으로 지정해 줘야 한다는 단점이 있다. 만약 MIME type을 지정하지 않고 업로드를 하게 되면 웹 브라우저가 Blob 스토리지에 저장된 이미지 파일을 렌더링하는 대신, 다운로드를 받으려 하니 반드시 주의하도록 하자.

여기서 이 MIME type을 지정하지 않은 채로 파일들을 옮기면서 **엄청난 삽질 한 번**.

그 다음에 한 일은 백업 받은 데이터베이스를 새로운 환경에 맞게 수정하는 일이었다. 하나의 데이터베이스에 두 사이트의 데이터들을 한꺼번에 밀어 넣으려니까 당연히 충돌이 날 수 밖에 없겠지. 워드프레스는 기본적으로 각각의 테이블에 `wp_` 접두사를 사용한다. 하지만, 지금은 두 개의 사이트가 서로 다른 테이블 접두사를 사용해야 하므로 하나는 `wp1_`, 다른 하나는 `wp2_`를 사용하기로 했다. 물론 실제로 저 접두사를 쓴 것은 아니다. 하지만, 이게 끝이 아니다. 테이블 접두사만 바꾸게 되면, 관리자 페이지에 접속할 수 없는 문제가 생기기 때문에 [이 포스트](https://wordpress.org/support/topic/wp-admin-you-do-not-have-sufficient-permissions-to-access-this-page#post-3693599)에서 언급한 바와 같이 `wp_user_roles`, `wp_capabilities`, `wp_user_level`, `wp_user-settings`, `wp_user-settings-time`, `wp_dashboard_quick_press_last_post_id` 값들을 찾아서 모두 `wp_` 부분을 `wp1_` 또는 `wp2_`로 바꿔주어야 했다.

**여기서 두번째 삽질**.

이렇게 수정한 데이터를 데이터베이스에 복원시키고 난 후, 파일들을 웹사이트에 업로드했다. 여기서 주의할 점은 아직 서브 디렉토리로 이동시키지 말아야 한다는 것. 기존의 사이트가 루트 디렉토리 기반이었으므로 우선은 파일들을 루트에 풀어줬다. 그리고 웹사이트 접속. 일단은 사이트가 제대로 돌아가는 것 처럼 보였다. 이제 관리자 화면에서 서브 디렉토리로 옮기는 것을 [이 페이지](https://codex.wordpress.org/Giving_WordPress_Its_Own_Directory#Moving_a_Root_install_to_its_own_directory)를 참고하여 진행했다.

**여기서 세번째 삽질**.

일단 여기까지 진행했으니 한 90% 정도는 성공했지 싶었다. 이제 Azure Blob Storage에 저장된 파일들로 기존의 링크를 다시 바꾸어 줄 차례가 됐다. 사실, 이 작업도 데이터베이스 복원 전에 해주는 것이 낫다. 이미 Blob Storage에 파일들이 옮겨가 있으니 말이다. 이건 단순히 `<img src="/wp-content/uploads/` 문자열 또는 `<img src="http://justinchronicles.net/wp-content/uploads/` 문자열을 `<img src="http://blob.justinchronicles.net/wp1`로 치환시켜 주면 되는 문제라서 큰 어려움은 없었다.

어쨌든 **여기서 네번째 삽질**.

마지막으로 [Windows Azure Storage for WordPress](https://wordpress.org/plugins/windows-azure-storage/) 플러그인을 추가한 후 API 키 값과 컨테이너를 설정해 주면 앞으로 저장하는 이미지들은 모두 Blob Storage를 이용하게 된다. 그런데, 이 플러그인을 설치하기 위해 관리자 화면으로 들어갈 때 [Jetpack](https://wordpress.org/plugins/jetpack/) 플러그인 충돌 때문에 관리자 화면이 나타나지 않는 경우가 있다. 이럴 땐, FTP로 접속해서 Jetpack 플러그인을 삭제하고 다시 설치하면 된다.

이걸로 **마지막 삽질**.

이렇게 해서 `justinchronicles.net` 블로그 사이트는 이전 완료!

### **6. `blog.aliencube.org` 사이트 복원**

이미 앞에서 수많은 삽질을 한 덕에 이것은 손쉽게 해결할 수 있었다. 같은 방법으로 복원했고, 추가적으로 삽질을 한 것들만을 나열해 보자면, 먼저 `Web.config` 파일을 통합하는 것이었다. 각각 갖고 있던 `Web.config` 파일들의 서로 다른 부분들을 합치는 것이었는데, 거의 대부분 URL Rewrite 규칙을 통합하는 것이어서 큰 어려움은 없었다.

두번째로는 루트 디렉토리의 `index.php` 파일을 수정하는 것이었다. 하나의 사이트만 있었을 때에는 아래와 같은 방법을 적용하면 손쉽게 해결이 가능했다. [이 페이지](https://codex.wordpress.org/Giving_WordPress_Its_Own_Directory#Moving_a_Root_install_to_its_own_directory) 참고

```php
require( dirname( __FILE__ ) . '/wp-blog-header.php' );

```

부분을 아래와 같이 수정했다.

```php
require( dirname( __FILE__ ) . '/wp1/wp-blog-header.php' );

```

하지만, 지금은 이렇게 `/wp1/`으로 하드코딩할 수 없고, 접속하는 URL에 따라 `/wp1/`을 호출할 지 아니면 `/wp2/`를 호출할 지 결정해야 하는 상황이다. 따라서, 아래와 같은 식으로 수정했다.

```php
$hostname = $_SERVER["HTTP_HOST"];
$subdir = "";
switch($hostname)
{
    case "justinchronicles.net":
    case "www.justinchronicles.net":
        $subdir = "wp1";
        break;
    case "blog.aliencube.org":
        $subdir = "wp2";
        break;
}

require( dirname( __FILE__ ) . '/'.$subdir.'/wp-blog-header.php' );

```

이렇게 조정함으로써, `justinchronicles.net`으로 접속할 경우에는 `wp1` 디렉토리 아래에 있는 블로그를 불러오고, `blog.aliencube.org`로 접속할 경우에는 `wp2` 디렉토리 아래에 있는 블로그를 불러오게 된다.

이것이 **마지막 삽질**.

이렇게 `blog.aliencube.org` 사이트도 이전 완료!

## 삽질 결과

워드프레스는 정말 손쉽게 사용할 수 있는 블로그 툴이긴 하다. 하지만, 뭔가 유지보수 측면에서는 굉장히 다양한 변수들을 고려하기에는 까다로울 수 있다는 점에서 사용하면서 주의가 필요하지 싶다. 이제 당분간 삽질은 그만~

그나저나 [AlienStrap](https://github.com/aliencube/Alienstrap-for-Wordpress) 테마도 손을 좀 봐야 할 텐데... [#귀찮아](https://twitter.com/hashtag/귀찮아)
