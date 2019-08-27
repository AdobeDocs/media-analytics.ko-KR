---
seo-title: Launch와 Media SDK 차이점 이해
title: Launch와 Media SDK 차이점 이해
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# Launch와 Media SDK 차이점 이해

## 기능 차이점

* *Launch* - Launch는 웹 기반 미디어 추적 솔루션을 설정, 구성 및 배포하면서 사용자를 안내하는 UI를 제공합니다. Launch는 DTM (다이내믹 태그 관리) 를 개선합니다.
* *Media SDK* - 미디어 SDK는 특정 플랫폼 (예: Android, iOS 등). Adobe는 모바일 앱에서 미디어 사용을 추적하기 위한 미디어 SDK를 권장합니다.

## 추적기 제작 차이점

### Launch

Launch는 추적 인프라를 만드는 두 가지 방법을 제공합니다. 두 방법 모두 Media Analytics 시작 확장 기능을 사용합니다.

1. 웹 페이지의 미디어 추적 API를 사용합니다.

   이 시나리오에서 미디어 분석 확장 기능은 미디어 추적 API를 전역 창 개체에서 구성된 변수로 내보냅니다.

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 다른 론치 익스텐션에서 미디어 추적 API를 사용합니다.

   이 시나리오에서는 `get-instance` 및 `media-heartbeat` 공유 모듈에 의해 노출된 미디어 추적 API를 사용합니다.

   >[!NOTE]
   >
   >공유 모듈은 웹 페이지에서 사용할 수 없습니다. 다른 확장의 공유 모듈만 사용할 수 있습니다.

   공유 모듈을 사용하여 `MediaHeartbeat` 인스턴스를 `get-instance` 만듭니다.
위임 개체를 노출 `get-instance``getQoSObject()` 및 `getCurrentPlaybackTime()` 함수로 전달합니다.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   공유 모듈을 통해 `MediaHeartbeat``media-heartbeat` 상수에 액세스.

### Media SDK

1. 개발 프로젝트에 미디어 분석 라이브러리를 추가합니다.
1. 구성 객체 (`MediaHeartbeatConfig`) 를 만듭니다.
1. `getQoSObject()` 및 `getCurrentPlaybackTime()` 함수를 노출하는 위임 프로토콜을 구현합니다.
1. 미디어 하트비트 인스턴스 (`MediaHeartbeat`) 를 만듭니다.

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

## 관련 설명서

### Launch

* [론치 개요](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [MA 익스텐션](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK

* [JS 설정](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

