---
title: 챕터 오프셋
description: 콘텐츠 내에 있는 챕터의 오프셋(시작 부분부터 초 단위)을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 6%

---


# 챕터 오프셋

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**챕터 오프셋**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [챕터 오프셋](/help/reporting/dimensions/chapter-offset.md)을 참조하십시오.*

>[!ENDSHADEBOX]

챕터 오프셋 변수는 컨텐츠 내에 있는 챕터의 오프셋으로서 시작부터 초 단위로 측정됩니다. 첫 번째 챕터에는 일반적으로 오프셋 `0`이(가) 있고, 후속 챕터에는 플레이헤드 시작 시간과 일치하는 오프셋이 있습니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.chapter.offset` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.chapter.offset` |
| **필수** | 아니요(모바일 SDK), 예(Edge, Media Collection API) |
| **전송 시점** | [챕터 시작](/help/implementation/events/chapters/chapter-start.md), 챕터 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.chapterDetails` 내에서 `offset`을(를) 설정합니다.

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

>[!TAB iOS]

오프셋을 네 번째 인수(`startTime`)로 `createChapterObject`에 전달합니다.

```swift
let chapterObject = Media.createChapterObjectWith(name: "Act II",
                                              position: 2,
                                                length: 360,
                                             startTime: 240)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

오프셋을 네 번째 인수(`startTime`)로 `createChapterObject`에 전달합니다.

```kotlin
val chapterObject = Media.createChapterObject("Act II",
                                              2L,
                                              360.0,
                                              240.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku Edge]

`media.chapterStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `xdm.mediaCollection.chapterDetails` 내에서 `offset`을(를) 설정합니다.

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

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.chapterDetails` 내에서 `offset`을(를) 사용하여 [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) 끝점을 호출합니다.

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

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

챕터 오프셋을 `ADBMobile.media.createChapterObject`에 네 번째 인수(`startTime`)로 전달합니다(초).

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length
  0                           // startTime (seconds from content start)
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Roku 2.x]

챕터 오프셋을 `adb_media_init_chapterinfo`에 네 번째 인수(`startTime`)로 전달합니다(초).

```brightscript
adb = ADBMobile()
chapterInfo = adb_media_init_chapterinfo("Pilot Episode - Opening", 1, 240.0, 0.0)  ' name, position, length, startTime

adb.mediaTrackEvent(adb.MEDIA_CHAPTER_START, chapterInfo)
```

>[!TAB 미디어 컬렉션 API]

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

>[!ENDTABS]
