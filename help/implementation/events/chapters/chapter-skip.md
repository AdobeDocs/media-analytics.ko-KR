---
title: 챕터 건너뛰기
description: 뷰어가 챕터를 건너뛰었다는 신호를 보냅니다.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 18%

---


# 챕터 건너뛰기

챕터 건너뛰기 이벤트는 뷰어가 완료되기 전에 챕터를 건너뛰었다는 신호를 보냅니다. 뷰어가 챕터 경계를 지나 완료될 때까지 관찰하지 않고 탐색할 때 보냅니다. 챕터가 끝까지 재생되면 [챕터 완료](chapter-complete.md)를 보냅니다.

* **필수 구성 요소**: [세션 시작](../session/session-start.md), [챕터 시작](chapter-start.md)
* **관련 지표**: 없음

## Web SDK

`eventType: "media.chapterSkip"`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

## Mobile SDK

`ChapterSkip` 이벤트 형식으로 `trackEvent`을(를) 호출합니다.

**iOS(Swift)**

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

**Android(Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

## Roku(BrightScript)

`eventType: "media.chapterSkip"`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterSkip",
        "mediaCollection": {
            "playhead": 60
        }
    }
})
```

## Media Edge API

[chapterSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterskip) 끝점을 호출합니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

`ChapterSkip` 이벤트 형식으로 `trackEvent` 호출:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

## Media Collection API

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `chapterSkip` POST 보내기:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```
