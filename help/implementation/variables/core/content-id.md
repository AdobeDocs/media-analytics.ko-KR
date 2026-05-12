---
title: 콘텐츠 ID
description: 미디어 콘텐츠를 고유하게 식별합니다.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 15%

---


# 콘텐츠 ID

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**콘텐츠 ID**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [콘텐츠](/help/reporting/dimensions/content.md)를 참조하세요.*

>[!ENDSHADEBOX]

컨텐츠 ID 변수는 각 미디어 컨텐츠를 고유하게 식별합니다. 모든 스트리밍 미디어 구현에 필요하며, 콘텐츠 보고 차원의 기본 키입니다. 세션 시작 시 설정하고 동일한 자산에 대해 모든 세션에서 안정적으로 유지합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.name` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **필수** | 예 |
| **전송 시점** | 세션 시작, 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `name`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
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

콘텐츠 ID를 `mediaId` 인수로 `createMediaObject`에 전달합니다.

**iOS(Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android(Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku(BrightScript)

`createMediaSession`을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `name`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
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

`mediaCollection.sessionDetails` 내에서 `name`(콘텐츠 ID)을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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

콘텐츠 ID를 두 번째 인수로 `ADB.Media.createMediaObject`에 전달합니다.

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name (friendly name)
  "video-123",              // media ID — Content ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`sessionStart` POST 요청의 `params` 개체에 `media.id` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.id": "video-123"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
