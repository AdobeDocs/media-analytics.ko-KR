---
title: 세션 종료
description: 뷰어가 콘텐츠를 중단하면 미디어 세션을 즉시 닫습니다.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 14%

---


# 세션 종료

세션 종료 이벤트는 미디어 추적 세션을 즉시 닫습니다. 뷰어가 끝에 도달하기 전에 컨텐츠를 중단하며 후속 이벤트가 동일한 세션에서 추적되지 않도록 하려는 경우 사용합니다. 뷰어가 콘텐츠를 마치면 대신 [세션 완료](session-complete.md)를 호출하십시오.

명시적인 세션 종료가 없으면 이벤트가 없는 경우 10분 또는 플레이헤드 이동이 없는 경우 30분 후에 세션이 자동으로 닫힙니다.

* **필수 구성 요소**: [세션 시작](session-start.md)
* **관련 지표**: 없음

## Web SDK

`eventType: "media.sessionEnd"`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

뷰어가 플레이어를 닫거나 다른 곳으로 이동하면 `trackSessionEnd`을(를) 호출합니다.

**iOS(Swift)**

```swift
tracker.trackSessionEnd()
```

**Android(Kotlin)**

```kotlin
tracker.trackSessionEnd()
```

## Roku(BrightScript)

`eventType: "media.sessionEnd"`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## Media Edge API

[sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend) 끝점 호출:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

뷰어가 플레이어를 닫거나 다른 곳으로 이동하면 `trackSessionEnd`을(를) 호출합니다.

```javascript
tracker.trackSessionEnd();
```

## Media Collection API

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `sessionEnd` POST 보내기:

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```
