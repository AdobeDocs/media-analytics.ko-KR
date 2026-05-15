---
title: 방송국
description: 오디오 브로드캐스트 콘텐츠의 라디오 방송국 이름 또는 ID를 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 16%

---


# 방송국

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**Station**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [Station](/help/reporting/dimensions/station.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

스테이션 변수는 오디오 콘텐츠를 브로드캐스트하는 라디오 방송국의 이름 또는 ID입니다(예: `"NPR"` 또는 `"WXYZ-FM"`). 이를 사용하여 신디케이트된 네트워크의 스테이션 간 참여를 비교할 수 있습니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.station` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.station`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.station` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `station`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        station: "NPR"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

스테이션을 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.AudioMetadataKeys.STATION` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.STATION] = "NPR"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.STATION] = "NPR"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku(BrightScript)

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `station`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "station": "NPR"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails` 내의 `station`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "station": "NPR"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.AudioMetadataKeys.Station`을(를) 사용하여 `contextData` 개체에 스테이션을 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Station] = "NPR";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`params` 개체에 `media.station` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.station": "NPR"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
