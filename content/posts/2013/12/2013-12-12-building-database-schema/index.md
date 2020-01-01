---
title: "데이터베이스 스키마 구상"
date: "2013-12-12"
slug: building-database-schema
description: ""
author: Justin-Yoo
tags:
- dotnet
- aliencube
- cms
- poc
- web
fullscreen: false
cover: ""
---

일단 컨셉은 [이전 포스트](/ko/2013/12/12/building-cms-concepts)에서와 같이 잡았고, 이제 해당 컨셉을 대략적인 ERD로 구성해 보았다.

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2013/12/PoC.Schema.Database.png)

- `PageSchemas`: 페이지를 구성하는 메타데이타를 저장한다. 향후 내부적으로 Strongly-typed object를 생성하기 위한 클라스 정의로도 쓰인다.
- `ElementGroups`: 페이지의 엘리먼트들을 묶어주는 메타데이타를 저장한다. 향후 내부적으로 Strongly-typed object를 생성하기 위한 서브클라스 정의로도 쓰인다.
- `ElementSchemas`: 페이지의 엘리먼트들을 구성하는 메타데이타를 저장한다. 향후 내부적으로 Strongly-typed object를 생성하기 위한 프로퍼티 정의로도 쓰인다.
- `ElementDataTypes`: 엘리먼트를 위한 데이타 타입에 해당하는 메타 데이타를 저장한다.
- `PredefinedElementDataValues`: 엘리먼트 데이타 타입들 중 드롭다운, 라디오버튼, 체크박스 등등 동적으로 생성할 때 필요한 데이타를 미리 지정한다.
- `Pages`: 실제 화면에 보이는 페이지에 대한 메타데이타를 저장한다.
- `PageVersions`: 페이지 데이타에 대한 버전관리를 한다.
- `PageElements`: 페이지 엘리먼트들에 대한 버전별 데이타를 저장한다.
- `PageContents`: 실제 페이지에 대한 통합 데이타를 XML 포맷과 JSON 포맷으로 저장한다.

더 필요한 몇가지 테이블이 있지 싶은데, 일단은 여기서부터 시작하는 걸로!
