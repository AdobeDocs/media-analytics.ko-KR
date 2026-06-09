---
title: 미디어 다운로드 플래그
description: 세션을 다운로드된 오프라인 재생으로 표시하여 스트리밍된 세션과 별도로 보고되도록 합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 5%

---


# 미디어 다운로드 플래그

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**미디어 다운로드 플래그**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [미디어 다운로드됨](/help/reporting/dimensions/media-downloaded-flag.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

미디어 다운로드 플래그는 세션이 인터넷의 라이브 스트림이 아니라 이전에 다운로드한 오프라인 콘텐츠의 재생임을 나타냅니다. 추적기(모바일 SDK)를 초기화할 때 설정하거나 `sessionStart` 페이로드(Edge/Media Collection API)에 포함하십시오. 이 플래그를 사용하여 보고에서 스트리밍된 세션으로부터 오프라인 재생을 구분합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.downloaded` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.downloaded` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.sessionDetails` 내에서 `isDownloaded`을(를) `true`(으)로 설정:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video",
        isDownloaded: true
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

추적기를 만들 때 `MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`을(를) 사용하여 추적기 구성에 다운로드한 콘텐츠 플래그를 설정합니다.

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

추적기를 만들 때 `MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`을(를) 사용하여 추적기 구성에 다운로드한 콘텐츠 플래그를 설정합니다.

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

val tracker = Media.createTracker(config)
```

>[!TAB Roku Edge]

`createMediaSession`을(를) 호출할 때 `xdm.mediaCollection.sessionDetails` 내에서 `isDownloaded`을(를) `true`(으)로 설정:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video",
                "isDownloaded": true
            },
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

장치가 온라인 상태가 되면 [downloaded](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/#downloaded) 끝점을 호출하여 `mediaDownloadedEvents` 내의 전체 오프라인 세션을 일괄 처리합니다. Adobe은 `isDownloaded`을(를) `true`(으)로 자동 설정하고 세션 ID를 할당합니다. 페이로드에 포함하지 마십시오.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.downloaded",
      "mediaDownloadedEvents": [
        {
          "mediaEventTimestamp": "YYYY-09-26T15:52:24+00:00",
          "mediaEventType": "media.sessionStart",
          "mediaCollection": {
            "sessionDetails": {
              "name": "video-123",
              "length": 128,
              "contentType": "vod",
              "playerName": "HTML5 Player",
              "channel": "Sports"
            },
            "playhead": 0
          }
        },
        {
          "mediaEventTimestamp": "YYYY-09-26T15:54:32+00:00",
          "mediaEventType": "media.sessionComplete",
          "mediaCollection": {
            "playhead": 128
          }
        }
      ]
    }
  }]
}
```

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

추적기를 만들기 전에 `ADB.MediaConfig`에 `downloadedContent`을(를) 설정합니다.

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";
mediaConfig.downloadedContent = true;

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

`trackSessionStart`을(를) 호출하기 전에 미디어 정보 개체에 `MediaDownloaded`을(를) 설정합니다.

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
mediaInfo[ADBMobile.media.MediaObjectKey.MediaDownloaded] = true;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

다운로드한 컨텐츠 추적은 Roku 2.x SDK에서 사용할 수 없습니다. 다운로드한 미디어 재생을 보고하려면 [Roku Edge SDK](/help/implementation/edge/roku.md) 또는 [Media Collection API](/help/implementation/analytics-only/media-collection-api.md)를 사용하십시오.

>[!TAB 미디어 컬렉션 API]

`sessionStart` POST 요청의 `params` 개체에 `media.downloaded` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.downloaded": true
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.

>[!ENDTABS]
