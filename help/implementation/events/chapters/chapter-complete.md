---
title: 챕터 완료
description: 챕터 세그먼트 재생이 완료되었음을 나타냅니다.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 11%

---


# 챕터 완료

챕터 완료 이벤트는 챕터 재생이 완료되었음을 나타냅니다. 뷰어가 챕터의 끝에 도달하면 보냅니다. 뷰어가 챕터를 건너뛸 경우 대신 [챕터 건너뛰기](chapter-skip.md)를 보냅니다.

* **필수 구성 요소**: [세션 시작](../session/session-start.md), [챕터 시작](chapter-start.md)
* **관련 지표**: [[!UICONTROL 챕터 완료]](/help/reporting/metrics/chapter-completes.md)

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

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

>[!TAB iOS]

`ChapterComplete` 이벤트 형식으로 `trackEvent`을(를) 호출합니다.

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

>[!TAB Android]

`ChapterComplete` 이벤트 형식으로 `trackEvent`을(를) 호출합니다.

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

>[!TAB Roku]

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

>[!TAB 미디어 Edge API]

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

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`ChapterComplete` 이벤트 형식으로 `trackEvent` 호출:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

>[!TAB Chromecast]

`ChapterComplete` 이벤트 형식으로 `trackEvent` 호출:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
```

>[!TAB 미디어 컬렉션 API]

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `chapterComplete` POST 보내기:

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```

>[!ENDTABS]
