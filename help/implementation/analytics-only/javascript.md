---
title: 스트리밍 미디어용 JavaScript 설정
description: Analytics 전용 스트리밍 미디어 구현을 위한 JavaScript(3.x)용 Media SDK을 설치하고 구성합니다.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 3%

---

# 스트리밍 미디어용 JavaScript 설정

JavaScript(3.x)용 Media SDK은 스트리밍 미디어 데이터를 Adobe Analytics으로 직접 전송합니다. 이 페이지에서는 JavaScript 수동 설치에 대해 설명합니다. 대신 태그를 통해 SDK을 배포하려면 [Media Analytics 태그 확장 설정](javascript-tags.md)을 참조하십시오. 새로운 구현의 경우 [웹 SDK](/help/implementation/edge/web-sdk.md)을(를) 사용하여 Edge Network 데이터스트림을 통해 Adobe Analytics으로 데이터를 전송하는 것이 좋습니다.

* **필수 구성 요소**:
   * [Analytics 전용 구현 개요](overview.md)를 완료합니다.
   * [AppMeasurement](https://experienceleague.adobe.com/ko/docs/analytics/implementation/js/overview) 및 [방문자 ID 서비스](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/appmeasurement)를 구현합니다.
   * [JavaScript용 Media SDK 다운로드](/help/getting-started/download-sdks.md).

## SDK 설치 및 구성

1. 모든 페이지에 액세스할 수 있는 웹 서버의 `MediaSDK.js`(다운로드한 `libs` 디렉터리) 호스트를 각 페이지에서 참조합니다.

   ```html
   <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH/MediaSDK.js"></script>
   ```

1. Media SDK을 페이지당 한 번씩 구성하여 필수 조건으로 설정한 `appMeasurement` 인스턴스를 전달합니다.

   ```js
   var mediaConfig = new ADB.MediaConfig();
   mediaConfig.trackingServer = "<media_collection_server>";
   mediaConfig.playerName = "player_name";
   mediaConfig.channel = "sample_channel";
   mediaConfig.appVersion = "app_version";
   mediaConfig.ssl = true;
   
   ADB.Media.configure(mediaConfig, appMeasurement);
   ```

   >[!NOTE]
   >
   >`mediaConfig.trackingServer` 변수는 **미디어 컬렉션 서버**&#x200B;입니다(예: `[namespace].hb-api.omtrdc.net`). 이 수집 서버는 AppMeasurement 인스턴스 내에 구성된 Analytics 추적 서버와 다릅니다.

1. `getInstance`을(를) 사용하여 추적기 인스턴스를 만듭니다. 전체 미디어 세션에 대한 인스턴스에 액세스할 수 있도록 유지:

   ```js
   var tracker = ADB.Media.getInstance();
   ```

## 미디어 이벤트 추적

추적기가 만들어진 상태에서 추적기 메서드를 사용하여 각 미디어 이벤트를 추적합니다. 정확한 호출은 각 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md) 페이지에서 **Media SDK JS 3.x** 탭을 참조하십시오.

## 다음 단계

구현이 완료되면 [Analytics 전용 구현에 대한 보고를 설정](/help/reporting/setup/analytics-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [JavaScript 3.x API용 Media SDK 참조](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/APIReference.md)
>* [JS SDK 2.x에서 3.x로 마이그레이션](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/MigrationGuide.md)
>* [Media Analytics 태그 확장 설정](javascript-tags.md)
>* [이벤트 개요](/help/implementation/events/overview.md)
