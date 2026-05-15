---
title: 컨텐츠 유형
description: 스트림 형식(VOD, 라이브, 선형, 팟캐스트, 노래 등)을 식별하려면 컨텐츠 유형을 설정하십시오.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 9%

---


# 컨텐츠 유형

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**콘텐츠 형식**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [콘텐츠 형식](/help/reporting/dimensions/content-type.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

콘텐츠 유형 변수는 스트림의 형식을 식별합니다(예: 비디오의 경우 VOD, 라이브 또는 선형, 오디오의 경우 팟캐스트 또는 오디오북). 모든 스트리밍 미디어 구현에 필요하며 세션 시작 시 설정해야 합니다. Adobe 정의 값이 기본 제공 콘텐츠 유형 세그먼트 및 보고서를 채웁니다. 사용자 지정 문자열도 허용되지만 기본 제공 세그먼트와 일치하지 않습니다. 설정하지 않으면 기본값은 `missing_content_type`입니다.

권장 값:

* **비디오:** `vod`, `live`, `linear`, `ugc`, `dvod`
* **오디오:** `song`, `podcast`, `audiobook`, `radio`

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.contentType` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.contentType` |
| **필수** | 예 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `contentType`을(를) 설정합니다.

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

콘텐츠 형식 상수를 `streamType` 인수로 `createMediaObject`에 전달합니다. `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`과(와) 같은 `MediaConstants.StreamType.*` 값을 사용합니다. 참고: Mobile SDK에서 `streamType` 인수는 콘텐츠 형식을 제어합니다. 스트림 유형 변수(오디오와 비디오)는 별도의 `mediaType` 인수입니다.

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

`createMediaSession`을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `contentType`을(를) 설정합니다.

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

`mediaCollection.sessionDetails` 내의 `contentType`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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

`ADB.Media.StreamType.*` 상수를 `ADB.Media.createMediaObject`에 네 번째 인수로 전달합니다.

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD, // Content type — VOD, LIVE, LINEAR, etc.
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`sessionStart` POST 요청의 `params` 개체에 `media.contentType` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.contentType": "vod"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
