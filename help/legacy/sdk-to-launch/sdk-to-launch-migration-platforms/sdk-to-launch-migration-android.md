---
title: “독립형 Media SDK에서 Adobe Launch로 마이그레이션 - Android”
description: Media SDK에서 Android용 Launch로 마이그레이션하는 방법에 대해 알아봅니다.
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 100%

---

# 독립형 Media SDK에서 Adobe Launch로 마이그레이션 - Android

>[!NOTE]
>Adobe Experience Platform Launch는 Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=ko-KR)를 참조하십시오.


## 구성

### 독립형 Media SDK

독립형 Media SDK에서는 앱에서 추적을 구성하고 추적기를 만들 때 SDK에 전달합니다.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0.0";
config.ovp = "video-provider";
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeat tracker = new MediaHeartbeat(... , config);
```

### Launch 확장

1. Experience Platform Launch에서 모바일 속성에 대한 [!UICONTROL 확장] 탭을 클릭합니다.
1. [!UICONTROL 카탈로그] 탭에서 오디오 및 비디오 확장용 Adobe Media Analytics 확장 프로그램을 찾은 후 [!UICONTROL 설치]를 클릭합니다.
1. 확장 설정 페이지에서 추적 매개 변수를 구성합니다.
Media 확장은 추적을 위해 구성된 매개 변수를 사용합니다.

![](assets/launch_config_mobile.png)

[모바일 확장 사용](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## 추적기 만들기

### 독립형 Media SDK

독립형 Media SDK에서는 `MediaHeartbeatConfig` 개체를 수동으로 만들고 추적 매개 변수를 구성합니다. `getQoSObject()` 및 `getCurrentPlaybackTime()functions.`를 노출하는 위임 인터페이스를 구현합니다.
추적할 `MediaHeartbeat` 인스턴스를 만듭니다.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0";
config.ovp = "video-provider";
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeatDelegate delegate = new MediaHeartbeatDelegate() {
    @Override
    public MediaObject getQoSObject() {
        // When called should return the latest qos values.
        return MediaHeartbeat.createQoSObject(<bitrate>,  
                                              <startupTime>,  
                                              <fps>,  
                                              <droppedFrames>);
    }

    @Override
    public Double getCurrentPlaybackTime() {
        // When called should return the current player time in seconds.
        return <currentPlaybackTime>;
    }

    MediaHeartbeat tracker = new MediaHeartbeat(delegate, config);
}
```

### Launch 확장

[Media API 참조 - 미디어 추적기 만들기](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

추적기를 만들기 전에 Media 확장 및 종속 확장을 모바일 코어에 등록해야 합니다.

```java
// Register the extension once during app launch
try {
    // Media needs Identity and Analytics extension
    // to function properly
    Identity.registerExtension();
    Analytics.registerExtension();

    // Initialize media extension.
    Media.registerExtension();                
    MobileCore.start(new AdobeCallback () {
        @Override
        public void call(Object o) {
            // Launch mobile property to pick extension settings.
            MobileCore.configureWithAppID("LAUNCH_MOBILE_PROPERTY");
        }
    });
} catch (InvalidInitException ex) {
    ...
}
```

Media 확장을 등록했으면 다음 API를 사용하여 추적기를 만듭니다.
추적기는 구성된 실행 속성에서 구성을 자동으로 선택합니다.

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

## 플레이헤드 및 경험 품질 값 업데이트.

### 독립형 Media SDK

독립형 Media SDK에서는 추적기를 만드는 동안 `MediaHeartbeartDelegate` 인터페이스를 구현하는 위임 개체를 전달합니다. 이 구현은 추적기가 `getQoSObject()` 및 `getCurrentPlaybackTime()` 인터페이스 메서드를 호출할 때마다 최신 QoE 플레이헤드를 반환해야 합니다.

### Launch 확장

이 구현은 추적기에 의해 노출된 `updateCurrentPlayhead` 메서드를 호출하여 현재 플레이어 플레이헤드를 업데이트해야 합니다. 정확한 추적을 위해 이 메서드를 초당 한 번 이상 호출해야 합니다.

[Media API 참조 - 현재 플레이어 업데이트](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

이 구현은 추적기에 의해 노출된 `updateQoEObject` 메서드를 호출하여 QoE 정보를 업데이트해야 합니다. 품질 지표가 변경될 때마다 이 메서드가 호출됩니다.

[Media API 참조 - QoE 개체 업데이트](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## 표준 미디어/광고 메타데이터 전달

### 독립형 Media SDK

* 표준 미디어 메타데이터:

   ```java
   MediaObject mediaInfo =
     MediaHeartbeat.createMediaObject("media-name",
                                      "media-id",
                                      60D,
                                      MediaHeartbeat.StreamType.VOD,
                                      MediaHeartbeat.MediaType.Video);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardVideoMetadata =
     new HashMap<String, String>();
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE,
                             "Sample Episode");
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW,
                             "Sample Show");
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON,
                             "Sample Season");
   mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata,
                      standardVideoMetadata);
   
   // Custom metadata keys
   HashMap<String, String> mediaMetadata = new HashMap<String, String>();
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* 표준 광고 메타데이터:

   ```java
   MediaObject adInfo =
     MediaHeartbeat.createAdObject("ad-name",
                                   "ad-id",
                                   1L,
                                   15D);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardAdMetadata =
     new HashMap<String, String>();
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER,
                          "Sample Advertiser");
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID,
                          "Sample Campaign");
   adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata,
                   standardAdMetadata);
   
   HashMap<String, String> adMetadata =
     new HashMap<String, String>();
   adMetadata.put("affiliate",
                  "Sample affiliate");
   
   tracker.trackEvent(MediaHeartbeat.Event.AdStart,
                      adObject,
                      adMetadata);
   ```

### Launch 확장

* 표준 미디어 메타데이터:

   ```java
   HashMap<String, Object> mediaObject =
     Media.createMediaObject("media-name",
                             "media-id",
                             60D,
                             MediaConstants.StreamType.VOD,
                             Media.MediaType.Video);
   
   HashMap<String, String> mediaMetadata =
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE,
                     "Sample Episode");
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW,
                     "Sample Show");
   
   // Custom metadata keys
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* 표준 광고 메타데이터:

   ```java
   HashMap<String, Object> adObject =
     Media.createAdObject("ad-name",
                          "ad-id",
                          1L,
                          15D);
   HashMap<String, String> adMetadata =
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER,
                  "Sample Advertiser");
   adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID,
                  "Sample Campaign");
   
   // Custom metadata keys
   adMetadata.put("affiliate",
                  "Sample affiliate");
   _tracker.trackEvent(Media.Event.AdStart,
                       adObject,
                       adMetadata);
   ```
