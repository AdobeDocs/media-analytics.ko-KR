---
title: 세션 종료
description: 뷰어가 콘텐츠를 중단하면 미디어 세션을 즉시 닫습니다.
feature: Streaming Media
role: Developer
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 8%

---


# 세션 종료

세션 종료 이벤트는 미디어 추적 세션을 즉시 및 비가역적으로 닫습니다. 세션 종료는 하드 클로즈입니다. 세션이 전송되면 세션이 종료되고 더 이상 이벤트를 추적할 수 없습니다. 플레이어가 소멸되거나 페이지가 언로드되는 경우와 같이 추가 이벤트가 발생하지 않을 것이 확실한 경우에만 세션 종료를 사용합니다. 대부분의 경우, 여전히 도착할 수 있는 이벤트를 차단할 위험을 감수하기보다는 자연스럽게 세션이 만료되도록 허용하는 것이 더 안전합니다. 뷰어가 콘텐츠를 마치면 대신 [세션 완료](session-complete.md)를 호출하십시오.

명시적인 세션 종료가 없으면 이벤트가 없는 경우 10분 또는 플레이헤드 이동이 없는 경우 30분 후에 세션이 자동으로 닫힙니다.

>[!NOTE]
>
>동일한 세션에 대해 세션 종료 를 두 번 이상 안전하게 호출할 수 있습니다. 백엔드는 첫 번째 이벤트에서 세션을 닫고 두 번째 세션 종료를 포함하여 해당 세션 ID에 대한 모든 후속 이벤트를 자동으로 삭제합니다. 뷰어가 플레이어를 닫을 때 30분 시간 초과가 만료되는 것과 같은 경합 조건에서 중복 호출을 방지할 필요는 없습니다.

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
