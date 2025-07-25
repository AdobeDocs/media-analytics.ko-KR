---
title: 독립형 Media SDK에서 Adobe Launch로 마이그레이션 - 웹(JS)
description: Media SDK에서 JS용 Launch로 마이그레이션하는 방법에 대해 알아봅니다.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 97%

---

# 독립형 Media SDK에서 Adobe Launch로 마이그레이션 - 웹(JS)

>[!NOTE]
>Adobe Experience Platform Launch는 Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=ko-KR)를 참조하십시오.

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

[Launch 사용 안내서 - Media 확장 설치 및 구성](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=ko#install-and-configure-the-ma-extension)

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

* [JavaScript 2.x 설정](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Launch 개요](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)
* [Media Analytics 확장](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=ko)
