---
title: 챕터 오프셋
description: 콘텐츠 내에 있는 챕터의 오프셋(시작 부분부터 초 단위)을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 12%

---


# 챕터 오프셋

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**챕터 오프셋**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [챕터 오프셋](/help/reporting/dimensions/chapter-offset.md)을 참조하십시오.*

>[!ENDSHADEBOX]

챕터 오프셋 변수는 컨텐츠 내에 있는 챕터의 오프셋으로서 시작부터 초 단위로 측정됩니다. 첫 번째 챕터에는 일반적으로 오프셋 `0`이(가) 있고, 후속 챕터에는 플레이헤드 시작 시간과 일치하는 오프셋이 있습니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.chapter.offset` |
| **XDM 컬렉션 필드** | [`mediaCollection.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **필수** | 아니요(모바일 SDK), 예(Edge, Media Collection API) |
| **전송 시점** | 챕터 시작, 챕터 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.chapterDetails` 내에서 `offset`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Act II",
        index: 2,
        offset: 240,
        length: 360
      },
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## Mobile SDK

오프셋을 네 번째 인수(`startTime`)로 `createChapterObject`에 전달합니다.

**iOS(Swift)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Act II",
                                              position: 2,
                                                length: 360,
                                             startTime: 240)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android(Kotlin)**

```kotlin
val chapterObject = Media.createChapterObject("Act II",
                                              2L,
                                              360.0,
                                              240.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku(BrightScript)

`media.chapterStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `mediaCollection.chapterDetails` 내에서 `offset`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Act II",
                "index": 2,
                "offset": 240,
                "length": 360
            },
            "playhead": 240
        }
    }
})
```

## Media Edge API

`mediaCollection.chapterDetails` 내에서 `offset`을(를) 사용하여 [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "index": 2,
          "offset": 240,
          "length": 360
        },
        "sessionID": "{sid}",
        "playhead": 240
      }
    }
  }]
}
```

## Media SDK

오프셋을 `ADB.Media.createChapterObject`에 네 번째 인수로 전달합니다.

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Act II",
  2,
  360,
  240
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## Media Collection API

`chapterStart` POST 요청의 `params` 개체에 `media.chapter.offset` 포함:

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.offset": 240
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
