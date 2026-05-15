---
title: 재생
description: 미디어 플레이어가 재생 상태에 들어왔다는 신호를 보냅니다.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 17%

---


# 재생

재생 이벤트는 미디어 플레이어가 재생 상태를 재생으로 변경했다는 신호를 보냅니다. 콘텐츠의 초기 시작 시, 자동 재생 시 및 일시 정지 또는 버퍼 이후 플레이어가 다시 시작될 때마다 전송합니다. 별도의 다시 시작 이벤트가 없습니다. [일시 중지 시작](pause-start.md) 또는 [버퍼 시작](buffer-start.md) 이후의 재생 이벤트가 다시 시작 이벤트로 사용됩니다.

* **필수 구성 요소**: [세션 시작](../session/session-start.md)
* **관련 지표**: [콘텐츠 시작](/help/reporting/metrics/content-starts.md)

## Web SDK

`eventType: "media.play"`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

미디어 플레이어가 재생을 시작하거나 다시 시작할 때 `trackPlay`을(를) 호출합니다.

**iOS(Swift)**

```swift
tracker.trackPlay()
```

**Android(Kotlin)**

```kotlin
tracker.trackPlay()
```

## Roku(BrightScript)

`eventType: "media.play"`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## Media Edge API

[play](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/) 끝점 호출:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

미디어 플레이어가 재생을 시작하거나 다시 시작할 때 `trackPlay`을(를) 호출합니다.

```javascript
tracker.trackPlay();
```

## Media Collection API

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `play` POST 보내기:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```
