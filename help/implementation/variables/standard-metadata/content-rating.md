---
title: 콘텐츠 등급
description: TV 유해 컨텐츠 가이드라인 또는 지역 등급 시스템으로 정의된 컨텐츠 등급을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 14%

---


# 콘텐츠 등급

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**콘텐츠 등급**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [콘텐츠 등급](/help/reporting/dimensions/content-rating.md)을 참조하세요.*

>[!ENDSHADEBOX]

콘텐츠 등급 변수는 TV 유해 콘텐츠 가이드라인(`"TVY"`, `"TVG"`, `"TVPG"`, `"TVMA"`) 또는 사용하는 지역 등급 시스템으로 정의된 대상 등급입니다. 등급 계층 간 참여 및 광고 로드를 비교하는 데 사용합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.rating` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.rating`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **필수** | 아니요 |
| **전송 시점** | 세션 시작, 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `rating`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        rating: "TVPG"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

HashMap 인수의 메타데이터 키로 등급을 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.RATING` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku(BrightScript)

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `rating`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "rating": "TVPG"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails` 내의 `rating`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "rating": "TVPG"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.VideoMetadataKeys.Rating`을(를) 사용하여 `contextData` 개체에 등급을 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Rating] = "TVPG";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`params` 개체에 `media.rating` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.rating": "TVPG"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
