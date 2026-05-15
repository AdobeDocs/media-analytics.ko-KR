---
title: 아티스트
description: 오디오 콘텐츠의 공연 아티스트 이름을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 16%

---


# 아티스트

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**아티스트**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대해서는 [아티스트](/help/reporting/dimensions/artist.md)를 참조하십시오.*

>[!ENDSHADEBOX]

Artist 변수는 오디오 콘텐츠에 대한 수행 중인 아티스트의 이름입니다(예: `"Crested Larks"`). 음악 또는 팟캐스트 세션에서 이를 사용하여 연주자의 참여를 중단합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.artist` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.artist`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.artist` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `artist`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        artist: "Crested Larks"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

아티스트 이름을 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.AudioMetadataKeys.ARTIST` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.ARTIST] = "Crested Larks"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.ARTIST] = "Crested Larks"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku(BrightScript)

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `artist`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "artist": "Crested Larks"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails` 내의 `artist`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "artist": "Crested Larks"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.AudioMetadataKeys.Artist`을(를) 사용하여 `contextData` 개체에 아티스트를 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Artist] = "Crested Larks";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`params` 개체에 `media.artist` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.artist": "Crested Larks"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
