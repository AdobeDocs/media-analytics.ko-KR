---
title: 측정 선택 사항
description: null
uuid: null
translation-type: ht
source-git-commit: 967a126723ebbbe02097bd07edc2ed967cd35f4c
workflow-type: ht
source-wordcount: '293'
ht-degree: 100%

---


# 측정 선택 사항{#measurement-options}

Adobe Media Analytics 확장, Media SDK 또는 Media Collection API와 함께 Adobe Launch를 사용하여 오디오 및 비디오 추적을 활성화할 수 있습니다.

## Adobe Media Analytics 확장이 있는 Adobe Launch

Adobe Launch는 Adobe의 차세대 tag management 솔루션입니다. Launch는 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 제공합니다. Launch와의 자체 통합을 구축하고 유지 관리하기 위해 확장을 사용합니다. 확장은 Launch UI 및 클라이언트 기능을 확장하는 JavaScript, HTML 및 CSS 패키지입니다. 자세한 내용은 [Experience Platform Launch 사용 안내서](https://docs.adobe.com/content/help/ko-KR/launch/using/overview.html)를 참조하십시오.

Adobe Media Analytics(MA) 확장은 오디오 및 비디오를 위한 핵심 JavaScript Media SDK(Media 2.x SDK)를 추가합니다. 이 확장은 Launch 사이트 또는 프로젝트에 `MediaHeartbeat` 추적기 인스턴스를 추가하는 기능을 제공합니다.

Media Analytics 확장을 사용하는 Adobe Launch를 사용하려면 다음 사항을 충족해야 합니다.
* Adobe Experience Cloud 고객이어야 합니다.
* 웹 페이지에 Launch 또는 DTM 포함 코드를 배포해야 합니다.
* [Analytics 확장](https://docs.adobe.com/content/help/ko-KR/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID 확장](https://docs.adobe.com/content/help/ko-KR/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

Media SDK는 가장 일반적으로 사용되는 미디어 플레이어와 통합됩니다.

## Media Collection API(RESTful API)

SDK 지원 없이 또는 SDK 통합이 필요하지 않으면 플레이어와 통합됩니다.<br>v2.2.0 릴리스부터 VHL(Video Heartbeat Library) SDK는 Media Analytics SDK로 이름을 바꿔 오디오 및 비디오 추적을 지원합니다. Media 2.2.0 SDK는 VHL 2.X SDK 시리즈와 완벽하게 호환됩니다. 이름 변경은 단순히 명명 규칙의 변경이며 기능 변경을 나타내지는 않습니다.
