---
title: 측정 선택 사항
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 967a126723ebbbe02097bd07edc2ed967cd35f4c
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 19%

---


# 측정 선택 사항{#measurement-options}

Adobe Media Analytics 확장 기능, Media SDK 또는 Media Collection API를 사용하여 Adobe Launch를 사용하여 오디오 및 비디오 추적을 활성화할 수 있습니다.

## Adobe Media Analytics 익스텐션을 사용한 Adobe Launch

Adobe Launch는 Adobe의 차세대 태그 관리 솔루션입니다. Launch를 사용하면 고객의 기대에 부응하는 경험을 제공하기 위해 필요한 모든 분석, 마케팅 및 광고 태그를 간단하게 배포 및 관리할 수 있습니다. Launch와의 통합을 구축하고 유지 관리하려면 익스텐션을 사용합니다. 확장자는 Launch UI 및 클라이언트 기능을 확장하는 JavaScript, HTML 및 CSS 패키지입니다. 자세한 내용은 [Experience Platform Launch 사용 안내서를 참조하십시오.](https://docs.adobe.com/content/help/ko-KR/launch/using/overview.html)

Adobe Media Analytics(MA) 익스텐션은 오디오 및 비디오용 핵심 JavaScript Media SDK(Media 2.x SDK)를 추가합니다. 이 확장은 Launch 사이트 또는 프로젝트에 `MediaHeartbeat` 추적기 인스턴스를 추가하는 기능을 제공합니다.

Media Analytics 확장 기능을 사용하는 Adobe Launch에는 다음이 필요합니다.
* Adobe Experience Cloud 고객이어야 합니다.
* 웹 페이지에 Launch 또는 DTM 포함 코드를 배포해야 합니다.
* [Analytics 확장](https://docs.adobe.com/content/help/ko-KR/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID 확장](https://docs.adobe.com/content/help/ko-KR/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

Media SDK는 가장 일반적으로 사용되는 미디어 플레이어와 통합됩니다.

## 미디어 컬렉션 API(RESTful API)

SDK 지원 없이 또는 SDK 통합이 필요하지 않은 경우 플레이어와 통합됩니다.<br>v2.2.0 릴리스부터 VHL(비디오 하트비트 라이브러리) SDK가 오디오 및 비디오 추적을 지원하기 위해 Media Analytics SDK로 이름이 변경되었습니다. Media 2.2.0 SDK는 VHL 2.x SDK 시리즈와 완전히 역호환됩니다. 이름 변경은 단순히 이름 지정 규칙의 변경 사항이며 기능 변경을 나타내지 않습니다.
