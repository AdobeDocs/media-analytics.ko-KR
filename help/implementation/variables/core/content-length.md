---
title: 콘텐츠 길이
description: 세션 시작 시 컨텐츠 길이(초)를 설정합니다. 진행률 표시기와 분당 평균 시청 시간을 유도합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 12%

---


# 콘텐츠 길이

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**콘텐츠 길이**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [콘텐츠 길이](/help/reporting/dimensions/content-length.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

콘텐츠 길이 변수는 콘텐츠의 총 기간(초)입니다. 모든 스트리밍 미디어 구현에 필요하며 세션 시작 시 설정해야 합니다. 컨텐츠 길이는 진행률 마커(10/25/50/75/95%) 및 분당 평균 시청 시간을 포함하여 여러 백엔드 계산 지표를 유도합니다. 컨텐츠 길이가 설정되지 않았거나 0보다 크지 않으면 해당 지표가 생성되지 않습니다. 알 수 없는 기간이 있는 라이브 스트림의 경우 `86400`(24시간)을 사용하십시오.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.length` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.length` |
| **필수** | 예 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `length`을(를) 설정합니다.

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

콘텐츠 길이를 `length` 인수로 `createMediaObject`에 전달합니다.

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

`createMediaSession`을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `length`을(를) 설정합니다.

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

`mediaCollection.sessionDetails` 내의 `length`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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

`ADB.Media.createMediaObject`에 세 번째 인수로 콘텐츠 길이를 초 단위로 전달합니다.

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,                      // length in seconds
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`sessionStart` POST 요청의 `params` 개체에 `media.length` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.length": 128
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
