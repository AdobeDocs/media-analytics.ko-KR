---
title: 상태 시작
description: 미디어 플레이어가 추적된 플레이어 상태로 들어왔다는 신호를 보냅니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 6%

---


# 상태 시작

상태 시작 이벤트는 미디어 플레이어가 전체 화면, 음소거 또는 자막 등 추적된 상태에 들어갔음을 나타냅니다. 플레이어는 동시에 여러 상태에 있을 수 있으며 상태는 동일한 이벤트 호출에서 시작되고 종료될 수 있습니다. [상태 끝](state-end.md) 이벤트로 각 상태를 닫으십시오.

올바른 상태 이름: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **필수 구성 요소**: [세션 시작](../session/session-start.md)
* **관련 지표**: 상태에 따라 다릅니다. [플레이어 상태 추적](/help/implementation/events/player-state/overview.md)을 참조하세요.

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

`eventType: "media.statesUpdate"` 및 `statesStart`의 상태 이름으로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

동일한 호출에서 여러 상태를 시작할 수 있습니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [
        { name: "fullscreen" },
        { name: "mute" }
      ],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

>[!TAB iOS]

적절한 `MediaConstants.PlayerState` 상수에서 만든 상태 개체에 `trackPlayerStateStart`을(를) 사용합니다.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateStart, info: stateObject, metadata: nil)
```

>[!TAB Android]

적절한 `MediaConstants.PlayerState` 상수에서 만든 상태 개체에 `trackPlayerStateStart`을(를) 사용합니다.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateStart, stateObject, null)
```

>[!TAB Roku Edge]

`eventType: "media.statesUpdate"` 및 `statesStart`의 상태 이름으로 `sendMediaEvent`을(를) 호출합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "fullscreen" }],
            "playhead": 60
        }
    }
})
```

>[!TAB 미디어 Edge API]

`statesStart`에서 상태 이름으로 [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) 끝점을 호출합니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60,
        "statesStart": [{ "name": "fullscreen" }]
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

적절한 `ADB.Media.PlayerState` 상수와 함께 `ADB.Media.createStateObject` 사용:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateStart(stateObject);
```

>[!TAB Chromecast]

적절한 `ADBMobile.media.PlayerState` 상수와 함께 `ADBMobile.media.createStateObject` 사용:

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
```

>[!TAB Roku 2.x]

플레이어 상태 추적은 Roku 2.x SDK에서 사용할 수 없습니다. 플레이어 상태를 추적하려면 [Roku Edge SDK](/help/implementation/edge/roku.md)를 사용하십시오.

>[!TAB 미디어 컬렉션 API]

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `stateStart` POST 보내기:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

>[!ENDTABS]
