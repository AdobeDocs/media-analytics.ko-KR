---
title: 상태 끝
description: 미디어 플레이어가 추적된 플레이어 상태를 종료했음을 신호로 보냅니다.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 13%

---


# 상태 끝

상태 종료 이벤트는 미디어 플레이어가 전체 화면, 음소거 또는 자막 등 추적된 상태를 종료했음을 알립니다. [상태 시작](state-start.md)에 의해 열린 상태를 닫도록 보냅니다. 상태는 동일한 이벤트 호출에서 시작되고 종료될 수 있습니다. 플레이어는 여러 상태를 동시에 종료할 수 있습니다.

올바른 상태 이름: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **필수 구성 요소**: [세션 시작](../session/session-start.md), [상태 시작](state-start.md)
* **관련 지표**: 상태에 따라 다릅니다. [플레이어 상태 추적](/help/use-cases/player-state-tracking/implementation-and-reporting.md)을 참조하세요.

## Web SDK

`eventType: "media.statesUpdate"` 및 `statesEnd`의 상태 이름으로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

상태는 동일한 호출에서 시작되고 종료될 수 있습니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

적절한 `MediaConstants.PlayerState` 상수에서 만든 상태 개체에 `trackPlayerStateEnd`을(를) 사용합니다.

**iOS(Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

**Android(Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

## Roku(BrightScript)

`eventType: "media.statesUpdate"` 및 `statesEnd`의 상태 이름으로 `sendMediaEvent`을(를) 호출합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "fullscreen" }],
            "playhead": 90
        }
    }
})
```

## Media Edge API

`statesEnd`에서 상태 이름으로 [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) 끝점을 호출합니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 90,
        "statesEnd": [{ "name": "fullscreen" }]
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

적절한 `ADB.Media.PlayerState` 상수와 함께 `ADB.Media.createStateObject` 사용:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateEnd(stateObject);
```

## Media Collection API

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `stateEnd` POST 보내기:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```
