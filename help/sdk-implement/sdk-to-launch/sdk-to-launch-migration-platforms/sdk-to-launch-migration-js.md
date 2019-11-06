---
seo-title: 독립 실행형 미디어 SDK에서 Adobe Launch - 웹(JS)으로 마이그레이션
title: 독립 실행형 미디어 SDK에서 Adobe Launch - 웹(JS)으로 마이그레이션
seo-description: Media SDK에서 Launch로 마이그레이션하는 데 도움이 되는 지침 및 코드 샘플입니다.
description: Media SDK에서 Launch로 마이그레이션하는 데 도움이 되는 지침 및 코드 샘플입니다.
translation-type: tm+mt
source-git-commit: b479f6623566b6a6989f625b757a97bba5f6aafd

---


# 독립 실행형 미디어 SDK에서 Adobe Launch - 웹(JS)으로 마이그레이션

## 기능 차이

* *시작* - 론치는 웹 기반 미디어 추적 솔루션의 설정, 구성 및 배포를 단계별로 안내하는 UI를 제공합니다. Launch는 DTM(다이내믹 태그 관리)을 통해 개선됩니다.
* *미디어 SDK* - 미디어 SDK는 특정 플랫폼(예:Android, iOS 등). Adobe에서는 모바일 앱의 미디어 사용을 추적하기 위해 Media SDK를 권장합니다.

## 구성

### 확장 실행

1. Experience Platform Launch에서 웹 [!UICONTROL 속성에] 대한 확장 탭을 클릭합니다.
1. 카탈로그 [!UICONTROL 탭에서] 오디오 및 비디오용 Adobe Media Analytics 확장 프로그램을 찾아 설치를 [!UICONTROL 클릭합니다].
1. 확장 설정 페이지에서 추적 매개 변수를 구성합니다.
미디어 확장자는 추적에 구성된 매개 변수를 사용합니다.

[사용 안내서 시작 - 미디어 확장 설치 및 구성](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

### 독립 실행형 미디어 SDK

독립 실행형 Media SDK에서는 추적기를 만들 때 앱에서 추적 구성을 구성하고 SDK에 전달합니다.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channe";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

구성 외에, 페이지가 제대로 작동하려면 `MediaHeartbeat` 미디어 추적에 대한 `AppMeasurement` 인스턴스와 `VisitorAPI` 인스턴스를 구성하고 전달해야 합니다.

## 추적기 제작의 차이점

### Launch

Launch는 추적 인프라를 만드는 두 가지 방법을 제공합니다. 두 방법 모두 Media Analytics Launch Extension을 사용합니다.

1. 웹 페이지에서 미디어 추적 API를 사용합니다.

   이 시나리오에서 Media Analytics 익스텐션은 미디어 추적 API를 전역 창 개체에 구성된 변수로 내보냅니다.

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 다른 Launch 확장의 미디어 추적 API를 사용합니다.

   이 시나리오에서는 미디어 추적 API를 사용하여 `get-instance` 및 공유 모듈을 `media-heartbeat` 노출합니다.

   >[!NOTE]
   >
   >공유 모듈은 웹 페이지에서 사용할 수 없습니다. 다른 확장 프로그램의 공유 모듈만 사용할 수 있습니다.

   공유 모듈을 사용하여 `MediaHeartbeat` 인스턴스를 `get-instance` 만듭니다.
위임 개체를 `get-instance` 노출과 `getQoSObject()` `getCurrentPlaybackTime()` 함수를 포함하는 위치로 전달합니다.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   공유 모듈을 통해 상수에 `MediaHeartbeat` `media-heartbeat` 액세스합니다.

### Media SDK

1. 개발 프로젝트에 미디어 분석 라이브러리를 추가합니다.
1. 구성 개체(`MediaHeartbeatConfig`)를 만듭니다.
1. 위임 프로토콜을 구현하여 `getQoSObject()` 및 `getCurrentPlaybackTime()` 함수를 노출합니다.
1. 미디어 하트비트 인스턴스 만들기(`MediaHeartbeat`).

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

[미디어 SDK - 추적기 제작](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html)

## 관련 설명서

### Launch

* [시작 개요](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [미디어 분석 확장](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK

* [JS 설정](/help/sdk-implement/setup/set-up-js.md)
* [미디어 SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

