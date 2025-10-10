---
title: Media Analytics SDK 다운로드 링크에 액세스
description: Android, iOS, JavaScript, Chromecast 및 Roku를 비롯한 사용 가능한 플랫폼에 대한 SDK 다운로드 링크입니다.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 81%

---

# Media SDK, 태그를 사용한 확장 기능 및 OTT SDK 가져오기 {#download-sdks}

이 페이지의 정보에는 최신 Media SDK를 다운로드하고 태그를 사용하는 미디어 확장 기능을 가져올 수 있는 링크가 포함되어 있습니다.

Adobe Experience Platform의 태그는 Adobe의 차세대 웹 사이트 태그 및 모바일 SDK 관리 기능입니다. 태그는 관련 고객 경험을 향상하는 데 필요한 분석, 마케팅 및 광고 솔루션을 배포하고 관리하는 간단한 방법을 제공합니다. 태그에 대한 자세한 내용은 [태그 개요](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=ko)를 참조하십시오.


>[!NOTE]
>
>기존 SDK 다운로드에 대한 자세한 내용은 [레거시—SDK 다운로드](/help/legacy/legacy-download-sdks.md)를 참조하십시오.<br>
>&#x200B;>지원 종료에 대한 중요한 정보는 [지원 종료 FAQ &#x200B;](/help/additional-resources/end-of-support-faqs.md)를 참조하십시오.

## Media SDK 및 모바일 라이브러리 {#media-sdks-libraries}

### 웹 구현 {#download-web-sdk}

| 지원되는 플랫폼 | 지원되는 솔루션 | 구현 방식 | 버전 |  API   |  설명서  |  샘플  |
|:---:|---|---|---|---| ---| ---|
| ![JavaScript 아이콘&#x200B;](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | Analytics 전용 | 웹 - «[JS v3.0.2용 Media SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [JavaScript API 참조](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [JavaScript을 사용하여 Media SDK 설치](/help/implementation/media-sdk/setup/web-implementation.md) | [JS v3.0.2용 Media SDK 샘플](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript 아이콘&#x200B;](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | Analytics 전용 | 웹 - 미디어 확장 기능 |  | [오디오 및 비디오 확장 기능용 Adobe Media Analytics(3.x SDK) — 태그 사용(데이터 수집)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=ko) | [오디오 및 비디오 확장 기능용 Adobe Media Analytics(3.x SDK) 샘플](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**웹** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | 웹 - Experience Platform Edge |  | [Edge Network을 사용하여 Customer Journey Analytics 스트리밍 미디어 컬렉션 구현](/help/implementation/edge/implementation-edge.md) <p>및</p><p>[Adobe Experience Platform Web SDK을 사용하여 Edge에 웹 데이터 보내기](/help/implementation/edge/edge-web-sdk.md)</p> | |

### 모바일 구현 {#get-mobile-extension}

| 지원되는 플랫폼 | 지원되는 솔루션 | 구현 방식 | 버전 |  설명서   |  샘플  |
|:---:|---|---|---|---|---|
| ![Android 아이콘&#x200B;](assets/android-icon.png)</br>**Android** | Adobe Analytics | Analytics 전용 | Android - 미디어 확장 기능 | [Mobile SDK 설명서](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - 오디오 및 비디오용 Media Analytics 샘플](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS 아이콘&#x200B;](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Analytics 전용 | iOS / tvOS - 미디어 확장 기능 | [Mobile SDK 설명서](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - 오디오 및 비디오용 Media Analytics 샘플](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Android 아이콘&#x200B;](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android - Experience Platform Edge | [JavaScript을 사용하여 Media SDK 설치](/help/implementation/edge/implementation-edge.md) | |
| ![Apple iOS 아이콘&#x200B;](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS / tvOS - Experience Platform Edge | [JavaScript을 사용하여 Media SDK 설치](/help/implementation/edge/implementation-edge.md) |  |

### OTT 구현 {#download-ott-libraries}

| 지원되는 플랫폼 | 지원되는 솔루션 | 구현 방식 | 버전 |  API   |  설명서  |
|:---:|---|---|---|---|---|
| ![Chromecast 아이콘&#x200B;](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Analytics 전용 | [Chromecast v3.0.3용 SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Chromecast API 참조](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Chromecast용 Mobile SDK v3.x 설정](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Roku 아이콘&#x200B;](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | Analytics 전용 | [Roku v2.2.6용 SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [Roku용 Mobile SDK v2.x 설정](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![Roku 아이콘&#x200B;](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [JavaScript을 사용하여 Media SDK 설치](/help/implementation/edge/implementation-edge.md) |
