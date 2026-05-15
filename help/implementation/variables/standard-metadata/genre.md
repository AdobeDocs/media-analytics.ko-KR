---
title: 장르
description: 콘텐츠 장르를 쉼표로 구분된 문자열로 설정합니다. 다중 장르 콘텐츠는 보고에서 라인 항목 간에 분할됩니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 12%

---


# 장르

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**Genre**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대해서는 [장르](/help/reporting/dimensions/genre.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

장르 변수는 제작자가 정의한 콘텐츠 장르입니다(예: `"Drama"`, `"Comedy"` 또는 `"Drama,Action"`). 콘텐츠가 두 개 이상의 장르에 맞는 경우 여러 값을 쉼표로 구분합니다. 보고에서 목록 변수는 각 값을 별도의 라인 항목으로 분할하고 각 라인 항목은 동일한 지표 가중치를 받습니다.

>[!NOTE]
>
>보고 파이프라인에서 장르 값이 `mediaReporting.sessionDetails.genreList`(목록 필드)으로 노출됩니다. 이전 `mediaReporting.sessionDetails.genre` 경로는 계속 작동하지만 `genreList`이(가) 권장됩니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.genre` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.genre`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.genre` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `genre`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        genre: "Drama,Action"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

장르 문자열을 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.GENRE` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku(BrightScript)

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `genre`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "genre": "Drama,Action"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails` 내의 `genre`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "genre": "Drama,Action"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.VideoMetadataKeys.Genre`을(를) 사용하여 `contextData` 개체에 장르 전달:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Genre] = "Drama,Action";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`params` 개체에 `media.genre` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.genre": "Drama,Action"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
