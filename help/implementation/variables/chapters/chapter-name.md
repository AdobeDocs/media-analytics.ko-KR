---
title: 챕터 이름
description: 챕터 제목별로 챕터 수준 보고를 분류할 수 있도록 각 챕터의 친숙한 이름을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 13%

---


# 챕터 이름

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**챕터 이름**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [챕터 이름](/help/reporting/dimensions/chapter-name.md)을 참조하세요.*

>[!ENDSHADEBOX]

챕터 이름 변수는 사람이 읽을 수 있는 챕터 제목입니다(예: `"Pilot Episode - Opening"`). 콘텐츠가 챕터로 나누어지는 모든 `media.chapterStart` 이벤트에 대해 설정합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.chapter.friendlyName` |
| **XDM 컬렉션 필드** | [`mediaCollection.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.chapter.friendlyName` |
| **필수** | 아니요 |
| **전송 시점** | [챕터 시작](/help/implementation/events/chapters/chapter-start.md), 챕터 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.chapterDetails` 내에서 `friendlyName`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Pilot Episode - Opening",
        index: 1,
        offset: 0,
        length: 240
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

챕터 이름을 첫 번째(`name`) 인수로 `createChapterObject`에 전달합니다.

**iOS(Swift)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android(Kotlin)**

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku(BrightScript)

`media.chapterStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `mediaCollection.chapterDetails` 내에서 `friendlyName`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Pilot Episode - Opening",
                "index": 1,
                "offset": 0,
                "length": 240
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.chapterDetails` 내에서 `friendlyName`을(를) 사용하여 [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "friendlyName": "Pilot Episode - Opening",
          "index": 1,
          "offset": 0,
          "length": 240
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

챕터 이름을 첫 번째 인수로 `ADB.Media.createChapterObject`에 전달합니다.

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## Media Collection API

`chapterStart` POST 요청의 `params` 개체에 `media.chapter.friendlyName` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
