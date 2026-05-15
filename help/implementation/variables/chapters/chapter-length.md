---
title: 챕터 길이
description: 각 챕터의 길이(초)를 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 13%

---


# 챕터 길이

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**챕터 길이**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대해서는 [챕터 길이](/help/reporting/dimensions/chapter-length.md)를 참조하십시오.*

>[!ENDSHADEBOX]

챕터 길이 변수는 챕터 기간(초)입니다. 모든 `media.chapterStart` 이벤트에 설정합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.chapter.length` |
| **XDM 컬렉션 필드** | [`mediaCollection.chapterDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.chapter.length` |
| **필수** | 아니요(모바일 SDK), 예(Edge, Media Collection API) |
| **전송 시점** | [챕터 시작](/help/implementation/events/chapters/chapter-start.md), 챕터 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.chapterDetails` 내에서 `length`을(를) 설정합니다.

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

챕터 길이를 세 번째 인수로 `createChapterObject`에 전달합니다(초).

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

`media.chapterStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `mediaCollection.chapterDetails` 내에서 `length`을(를) 설정합니다.

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

`mediaCollection.chapterDetails` 내에서 `length`을(를) 사용하여 [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
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

챕터 길이를 세 번째 인수로 `ADB.Media.createChapterObject`에 전달합니다.

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",
  1,
  240,
  0
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## Media Collection API

`chapterStart` POST 요청의 `params` 개체에 `media.chapter.length` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.length": 240
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
