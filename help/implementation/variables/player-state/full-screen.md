---
title: 전체 화면
description: 백엔드가 전체 화면 참여를 보고할 수 있도록 뷰어가 전체 화면 재생에 들어가고 종료되는 시기를 추적합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 6%

---


# 전체 화면

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**전체 화면**&#x200B;플레이어 상태에 대한 데이터 수집을 다룹니다. 해당 보고 지표에 대해 [전체 화면의 영향을 받은 스트림](/help/reporting/metrics/full-screen-streams-impacted.md), [전체 화면 카운트](/help/reporting/metrics/full-screen-count.md) 및 [전체 화면 총 기간](/help/reporting/metrics/full-screen-total-duration.md)을 참조하세요.*

>[!ENDSHADEBOX]

전체 화면 플레이어 상태는 뷰어가 전체 화면 재생에 들어오고 나갈 때 추적됩니다. 뷰어가 전체 화면에 들어갈 때마다 상태 시작 이벤트를 실행하고 뷰어가 나갈 때는 상태 종료 이벤트를 실행합니다. 백엔드는 이러한 이벤트에서 영향을 받은 스트림, 상태 항목의 수 및 총 상태 시간 등 세 가지 지표를 계산합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.states.fullscreen.set`, `a.media.states.fullscreen.count`, `a.media.states.fullscreen.time` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/media-collection-details) 및 [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/media-collection-details)&#x200B;(`name: "fullscreen"`이(가) 있는 항목) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.states.fullscreen.set`, `c_contextdata.a.media.states.fullscreen.count`, `c_contextdata.a.media.states.fullscreen.time` |
| **필수** | 아니요 |
| **전송 시점** | [상태 시작](/help/implementation/events/player-state/state-start.md), [상태 끝](/help/implementation/events/player-state/state-end.md) |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 사용하여 상태가 `statesStart`에 추가된 `media.statesUpdate` 이벤트를 보냅니다.

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

뷰어가 전체 화면을 종료하면 `statesEnd` 상태의 다른 이벤트를 보냅니다.

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

>[!TAB iOS]

`MediaConstants.PlayerState.FULLSCREEN` 상수와 함께 `tracker.trackPlayerStateStart()` 및 `tracker.trackPlayerStateEnd()`을(를) 사용합니다.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(info: stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

`MediaConstants.PlayerState.FULLSCREEN` 상수와 함께 `tracker.trackPlayerStateStart()` 및 `tracker.trackPlayerStateEnd()`을(를) 사용합니다.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku Edge]

`sendMediaEvent`을(를) 사용하여 상태가 `statesStart`에 추가된 `media.statesUpdate` 이벤트를 보냅니다.

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

뷰어가 전체 화면을 종료하면 `statesEnd` 상태의 다른 이벤트를 보냅니다.

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

>[!TAB 미디어 Edge API]

`statesStart`(또는 뷰어가 종료되면 `statesEnd`)에서 `fullscreen`(으)로 [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "fullscreen" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`ADB.Media.createStateObject` 및 `ADB.Media.PlayerState.FullScreen` 상수 사용:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);

tracker.trackPlayerStateStart(stateObject);
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Chromecast에는 `PlayerState` 상수가 없으므로 `"fullscreen"` 문자열과 함께 `ADBMobile.media.createStateObject`을(를) 직접 사용하십시오.

```javascript
var stateObject = ADBMobile.media.createStateObject("fullscreen");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the user exits full-screen:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

플레이어 상태 추적은 Roku 2.x SDK에서 사용할 수 없습니다. 플레이어 상태를 추적하려면 [Roku Edge SDK](/help/implementation/edge/roku.md)를 사용하십시오.

>[!TAB 미디어 컬렉션 API]

뷰어가 전체 화면으로 들어가면 `stateStart` POST 요청을 보내고, 뷰어가 종료되면 `stateEnd` POST를 보냅니다.

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523850000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.

>[!ENDTABS]
