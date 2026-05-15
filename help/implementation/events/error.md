---
title: 오류
description: 미디어 플레이어에 오류가 발생했음을 나타냅니다.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 16%

---


# 오류

오류 이벤트는 미디어 플레이어에 오류가 발생했음을 나타냅니다. 오류를 추적해도 세션이 닫히지 않습니다. 오류가 발생하여 재생을 계속할 수 없는 경우 오류 이벤트 후에 [세션 종료](session/session-end.md)를 호출하십시오.

* **필수 구성 요소**: [세션 시작](session/session-start.md)
* **관련 지표**: [오류 영향을 받은 스트림](/help/reporting/metrics/error-impacted-streams.md)

`errorDetails.source` 속성은 두 개의 값만 허용합니다. `player`(미디어 플레이어에서 발생한 오류)와 `external`(CDN 또는 네트워크와 같은 외부 소스에서 발생한 오류).

## Web SDK

`eventType: "media.error"` 및 필수 `errorDetails`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

오류 ID 문자열로 `trackError`을(를) 호출합니다.

**iOS(Swift)**

```swift
tracker.trackError(errorId: "media-error-001")
```

**Android(Kotlin)**

```kotlin
tracker.trackError("media-error-001")
```

## Roku(BrightScript)

`eventType: "media.error"` 및 필수 `errorDetails`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

## Media Edge API

필요한 `errorDetails`(으)로 [오류](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/) 끝점을 호출합니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

오류 ID 문자열로 `trackError`을(를) 호출합니다.

```javascript
tracker.trackError("media-error-001");
```

## Media Collection API

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `error` POST 보내기:

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```
