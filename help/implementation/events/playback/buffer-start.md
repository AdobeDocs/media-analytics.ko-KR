---
title: 버퍼 시작
description: 미디어 플레이어가 버퍼링 상태에 들어갔음을 알립니다.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 8%

---


# 버퍼 시작

버퍼 시작 이벤트는 미디어 플레이어가 버퍼링 상태에 들어갔음을 알립니다.

* **필수 구성 요소**: [세션 시작](../session/session-start.md)
* **관련 지표**: [[!UICONTROL 버퍼 이벤트]](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**XDM 기반 API(Web SDK, Roku, Media Edge API, Media Collection API):** 버퍼 다시 시작 이벤트 유형이 없습니다. `bufferStart` 이후에 [`play`](play.md) 이벤트를 보낼 때 버퍼 끝이 추론됩니다.
>
>**Mobile SDK:** 플레이어가 버퍼링을 종료하면 `trackEvent(BufferComplete)`을(를) 호출한 다음 `trackPlay()`을(를) 호출하여 재생을 다시 시작합니다.

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

`eventType: "media.bufferStart"`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bufferStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

플레이어가 버퍼링 상태가 되면 `BufferStart`(으)로 `trackEvent`을(를) 호출하고 종료되면 `BufferComplete`을(를) 호출합니다.

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

>[!TAB Android]

플레이어가 버퍼링 상태가 되면 `BufferStart`(으)로 `trackEvent`을(를) 호출하고 종료되면 `BufferComplete`을(를) 호출합니다.

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

>[!TAB Roku]

`eventType: "media.bufferStart"`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

>[!TAB 미디어 Edge API]

[bufferStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bufferstart/) 끝점 호출:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bufferStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bufferStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
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

`BufferStart` 이벤트 형식으로 `trackEvent` 호출:

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

>[!TAB Chromecast]

플레이어가 버퍼링 상태가 되면 `BufferStart`(으)로 `trackEvent`을(를) 호출하고 종료되면 `BufferComplete`을(를) 호출합니다.

```javascript
// Buffer starts
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);

// Buffer ends
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
```

>[!TAB 미디어 컬렉션 API]

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `bufferStart` POST 보내기:

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```

>[!ENDTABS]
