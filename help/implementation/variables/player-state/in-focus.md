---
title: 포커스
description: 백엔드가 포커스 참여를 보고할 수 있도록 플레이어가 뷰어의 화면에 포커스가 있는 시기를 추적합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 5%

---


# 포커스

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**포커스 있음**&#x200B;플레이어 상태에 대한 데이터 수집을 다룹니다. 해당 보고 지표에 대해서는 [초점의 영향을 받은 스트림](/help/reporting/metrics/in-focus-streams-impacted.md), [초점 카운트](/help/reporting/metrics/in-focus-count.md) 및 [초점 총 기간](/help/reporting/metrics/in-focus-total-duration.md)을 참조하십시오.*

>[!ENDSHADEBOX]

플레이어가 시청자의 주의를 끌 때 포커스 중인 플레이어 상태가 추적됩니다. 플레이어가 포커스를 얻으면(일반적으로 플레이어 탭이나 창이 활성화될 때) 상태 시작 이벤트를 실행하고 플레이어가 포커스를 잃으면 상태 종료 이벤트를 실행합니다. 백엔드는 이러한 이벤트에서 영향을 받은 스트림, 상태 항목의 수 및 총 상태 시간 등 세 가지 지표를 계산합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.states.infocus.set`, `a.media.states.infocus.count`, `a.media.states.infocus.time` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) 및 [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details)&#x200B;(`name: "inFocus"`이(가) 있는 항목) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.states.infocus.set`, `c_contextdata.a.media.states.infocus.count`, `c_contextdata.a.media.states.infocus.time` |
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
      statesStart: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

플레이어가 포커스를 잃으면 상태가 `statesEnd`인 다른 이벤트를 보냅니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

`MediaConstants.PlayerState.IN_FOCUS` 상수와 함께 `tracker.trackPlayerStateStart()` 및 `tracker.trackPlayerStateEnd()`을(를) 사용합니다.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

`MediaConstants.PlayerState.IN_FOCUS` 상수와 함께 `tracker.trackPlayerStateStart()` 및 `tracker.trackPlayerStateEnd()`을(를) 사용합니다.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku Edge]

`sendMediaEvent`을(를) 사용하여 상태가 `statesStart`에 추가된 `media.statesUpdate` 이벤트를 보냅니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "inFocus" }],
            "playhead": 60
        }
    }
})
```

플레이어가 포커스를 잃으면 상태가 `statesEnd`인 다른 이벤트를 보냅니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "inFocus" }],
            "playhead": 90
        }
    }
})
```

>[!TAB 미디어 Edge API]

`statesStart`(또는 플레이어가 포커스를 잃으면 `statesEnd`)에서 `inFocus`(으)로 [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "inFocus" }],
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

`ADB.Media.createStateObject` 및 `ADB.Media.PlayerState.InFocus` 상수 사용:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.InFocus);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Chromecast에는 `PlayerState` 상수가 없으므로 `"inFocus"` 문자열과 함께 `ADBMobile.media.createStateObject`을(를) 직접 사용하십시오.

```javascript
var stateObject = ADBMobile.media.createStateObject("inFocus");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the player loses focus:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

플레이어 상태 추적은 Roku 2.x SDK에서 사용할 수 없습니다. 플레이어 상태를 추적하려면 [Roku Edge SDK](/help/implementation/edge/roku.md)를 사용하십시오.

>[!TAB 미디어 컬렉션 API]

플레이어가 포커스를 얻으면 `stateStart` POST 요청을 보내고 포커스를 잃으면 `stateEnd` POST를 보냅니다.

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "inFocus"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.

>[!ENDTABS]
