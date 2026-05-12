---
title: 스트림 유형
description: 스트림 유형을 설정하여 미디어 스트림이 오디오 콘텐츠인지 비디오 콘텐츠인지 식별합니다.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 10%

---


# 스트림 유형

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**스트림 형식**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [스트림 유형](/help/reporting/dimensions/stream-type.md)을 참조하세요.*

>[!ENDSHADEBOX]

스트림 유형 변수는 미디어 스트림이 오디오 콘텐츠인지 비디오 콘텐츠인지를 식별합니다. 모든 스트리밍 미디어 구현에 필요하며, 모든 미디어 세션의 시작 시 설정해야 합니다.

스트림 유형을 올바르게 설정하는 것은 스트리밍 미디어 보고의 기본입니다. Adobe Analytics의 기본 제공 **미디어 스트림 유형** 세그먼트(모든 미디어, 오디오만, 비디오만)를 사용하도록 설정하고 Customer Journey Analytics에서 별도의 오디오 및 비디오 보고를 구동합니다. 또한 세션 데이터가 Media Analytics 파이프라인 전체에서 올바르게 분류되도록 합니다. 설정되지 않았거나 잘못된 스트림 유형의 세션은 다운스트림 보고에서 그룹 해제되거나 잘못 분류될 수 있습니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.streamType` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **필수** | 예 |
| **전송 시점** | 세션 시작, 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `streamType`을(를) 설정합니다.

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

`Media.MediaType.Video` 또는 `Media.MediaType.Audio`을(를) `createMediaObject`에 `mediaType` 인수로 전달합니다. `createMediaObject`의 `streamType` 인수는 이 변수가 아닌 콘텐츠 형식 변수(VOD, Live 등)를 제어합니다.

**iOS(Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                                id: "video-id",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android(Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("video-123",
                                        "video-id",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku(BrightScript)

`createMediaSession`을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `streamType`을(를) 설정합니다.

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

`mediaCollection.sessionDetails` 내의 `streamType`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "channel": "Sports",
          "streamType": "video"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.MediaType.Video` 또는 `ADB.Media.MediaType.Audio`을(를) `Media.createMediaObject`에 다섯 번째 인수로 전달합니다.

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name
  "video-123",              // media ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD, // content type
  ADB.Media.MediaType.Video // stream type: Video or Audio
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`sessionStart` POST 요청의 `params` 개체에 `media.streamType` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamType": "video"
  }
}
```

전체 요청 구조 및 모든 필수 필드에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
