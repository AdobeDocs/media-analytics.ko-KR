---
title: '"독립형 Media SDK에서 Launch로 마이그레이션 - 웹(JS)"'
description: Media SDK에서 JS용 Launch로 마이그레이션하는 방법을 알아봅니다.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 91%

---

# 독립형 Media SDK에서 Adobe Launch로 마이그레이션 - 웹(JS)

## 기능 차이점

* *Launch* - Launch는 웹 기반 미디어 추적 솔루션 설정, 구성 및 배포를 단계별로 안내하는 UI를 제공합니다. Launch는 DTM(Dynamic Tag Management)을 통해 개선됩니다.
* *Media SDK* - Media SDK는 특정 플랫폼(예: Android, iOS 등)용으로 설계된 미디어 추적 라이브러리를 제공합니다. 모바일 앱에서 미디어 사용을 추적하는 데 Media SDK를 사용하는 것이 좋습니다.

## 구성

### 독립형 Media SDK

독립형 Media SDK에서는 앱에서 추적 구성을 지정하고 추적기를 만들 때 SDK에 전달합니다.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

미디어 추적이 제대로 작동하려면 `MediaHeartbeat` 구성 외에도 미디어 추적에 대한 `AppMeasurement` 인스턴스와 `VisitorAPI` 인스턴스를 페이지에서 구성하고 전달해야 합니다.

### Launch 확장

1. Experience Platform Launch에서 웹 속성에 대한 [!UICONTROL 확장] 탭을 클릭합니다.
1. [!UICONTROL 카탈로그] 탭에서 오디오 및 비디오 확장용 Adobe Media Analytics 확장 프로그램을 찾은 후 [!UICONTROL 설치]를 클릭합니다.
1. 확장 설정 페이지에서 추적 매개 변수를 구성합니다.
Media 확장은 추적을 위해 구성된 매개 변수를 사용합니다.

   ![](assets/launch_config_js.png)

[Launch 사용 안내서 - Media 확장 설치 및 구성](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

## 추적기 만들기의 차이점

### Media SDK

1. 개발 프로젝트에 Media Analytics 라이브러리를 추가합니다.
1. 구성 개체(`MediaHeartbeatConfig`)를 만듭니다.
1. `getQoSObject()` 및 `getCurrentPlaybackTime()` 함수를 노출하는 위임 프로토콜을 구현합니다.
1. 미디어 하트비트 인스턴스(`MediaHeartbeat`)를 만듭니다.

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

<!--  Dead Link - from 2019 - can't locate where this should go
[Media SDK - Tracker Creation](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html) -->

### Launch

Launch는 추적 인프라를 만드는 두 가지 방법을 제공합니다. 두 방법 모두 Media Analytics Launch 확장을 사용합니다.

1. 웹 페이지의 미디어 추적 API를 사용합니다.

   이 시나리오에서 Media Analytics 확장은 미디어 추적 API를 전역 창 개체에 구성된 변수로 내보냅니다.

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 다른 Launch 확장의 미디어 추적 API를 사용합니다.

   이 시나리오에서는 `get-instance` 및 `media-heartbeat` 공유 모듈에 의해 노출된 미디어 추적 API를 사용합니다.

   >[!NOTE]
   >
   >공유 모듈은 웹 페이지에서 사용할 수 없습니다. 다른 확장 프로그램의 공유 모듈만 사용할 수 있습니다.

   `get-instance` 공유 모듈을 사용하여 `MediaHeartbeat` 인스턴스를 만듭니다.
`getQoSObject()` 및 `getCurrentPlaybackTime()` 함수를 노출하는 `get-instance`에 위임 개체를 전달합니다.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   `media-heartbeat` 공유 모듈을 통해 `MediaHeartbeat` 상수에 액세스합니다.

## 관련 설명서

### Media SDK

* [JavaScript 2.x 설정](/help/sdk-implement/setup/setup-javascript/set-up-js-2.md)
* [JavaScript 3.x 설정](/help/sdk-implement/setup/setup-javascript/set-up-js-3.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Launch 개요](https://experienceleague.adobe.com/docs/launch/using/overview.html?lang=kr)
* [Media Analytics 확장](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
