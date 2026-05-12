---
title: 콘텐츠 채널
description: 콘텐츠가 재생되는 배포 스테이션, 네트워크 또는 속성을 식별하도록 채널을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 12%

---


# 콘텐츠 채널

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**콘텐츠 채널**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [콘텐츠 채널](/help/reporting/dimensions/content-channel.md)을 참조하세요.*

>[!ENDSHADEBOX]

콘텐츠 채널 변수는 콘텐츠가 재생되는 배포 스테이션, 네트워크 또는 속성을 식별합니다. 모든 스트리밍 미디어 구현에 필요합니다. 모든 문자열이 허용됩니다. 일반적인 값에는 네트워크 이름, 사이트 경로의 일부 또는 내부 속성 식별자가 포함됩니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.channel` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **필수** | 예 |
| **전송 시점** | 세션 시작, 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `channel`을(를) 설정합니다.

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
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

추적기를 만들 때 `MediaConstants.TrackerConfig.CHANNEL`을(를) 사용하여 추적기 구성을 통해 채널을 설정합니다. 채널이 미디어 개체의 일부가 아닙니다.

**iOS(Swift)**

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

**Android(Kotlin)**

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

## Roku(BrightScript)

`createMediaSession`을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `channel`을(를) 설정합니다.

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
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails` 내의 `channel`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
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
    }
  }]
}
```

## Media SDK

추적기를 만들기 전에 `ADB.MediaConfig`에서 채널을 설정하십시오.

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

## Media Collection API

`sessionStart` POST 요청의 `params` 개체에 `media.channel` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
