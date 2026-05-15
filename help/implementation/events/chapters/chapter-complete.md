---
title: 챕터 완료
description: 챕터 세그먼트 재생이 완료되었음을 나타냅니다.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 20%

---


# 챕터 완료

챕터 완료 이벤트는 챕터 재생이 완료되었음을 나타냅니다. 뷰어가 챕터의 끝에 도달하면 보냅니다. 뷰어가 챕터를 건너뛸 경우 대신 [챕터 건너뛰기](chapter-skip.md)를 보냅니다.

* **필수 구성 요소**: [세션 시작](../session/session-start.md), [챕터 시작](chapter-start.md)
* **관련 지표**: [챕터 완료](/help/reporting/metrics/chapter-completes.md)

## Web SDK

`eventType: "media.chapterComplete"`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## Mobile SDK

`ChapterComplete` 이벤트 형식으로 `trackEvent`을(를) 호출합니다.

**iOS(Swift)**

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

**Android(Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

## Roku(BrightScript)

`eventType: "media.chapterComplete"`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterComplete",
        "mediaCollection": {
            "playhead": 240
        }
    }
})
```

## Media Edge API

[chapterComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chaptercomplete) 끝점 호출:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 240
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

`ChapterComplete` 이벤트 형식으로 `trackEvent` 호출:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

## Media Collection API

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `chapterComplete` POST 보내기:

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```
