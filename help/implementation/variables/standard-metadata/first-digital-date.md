---
title: 최초 디지털 날짜
description: 디지털 플랫폼에서 컨텐츠가 처음 방송된 날짜를 설정합니다. Adobe에서는 YYYY-MM-DD 형식을 권장합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 13%

---


# 최초 디지털 날짜

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**첫 번째 디지털 날짜**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대해서는 [첫 번째 디지털 날짜](/help/reporting/dimensions/first-digital-date.md)를 참조하십시오.*

>[!ENDSHADEBOX]

첫 번째 디지털 날짜 변수는 컨텐츠가 디지털 플랫폼에서 처음으로 방송된 날짜입니다. 모든 날짜 형식이 허용되지만, Adobe에서는 일관성을 위해 `YYYY-MM-DD`을(를) 권장합니다. [첫 방송 날짜](/help/implementation/variables/standard-metadata/first-air-date.md)와 함께 사용하여 디지털 릴리스 시기를 원본 브로드캐스트와 비교합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.digitalDate` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.digitalDate` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `firstDigitalDate`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstDigitalDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

HashMap 인수의 메타데이터 키로 첫 번째 디지털 날짜를 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku(BrightScript)

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `firstDigitalDate`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstDigitalDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails` 내의 `firstDigitalDate`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "firstDigitalDate": "2016-01-25"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.VideoMetadataKeys.FirstDigitalDate`을(를) 사용하여 `contextData` 개체에서 첫 번째 디지털 날짜를 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstDigitalDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`params` 개체에 `media.firstDigitalDate` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstDigitalDate": "2016-01-25"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
