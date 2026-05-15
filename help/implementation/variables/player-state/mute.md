---
title: 음소거
description: 뷰어가 오디오를 음소거하고 음소거를 해제하는 시점을 추적하여 백엔드가 음소거 참여를 보고할 수 있도록 합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 10%

---


# 음소거

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**음소거**플레이어 상태에 대한 데이터 수집을 다룹니다. 해당 보고 지표에 대해 [음소거의 영향을 받은 스트림](/help/reporting/metrics/mute-streams-impacted.md), [음소거 카운트](/help/reporting/metrics/mute-count.md) 및 [음소거 총 기간](/help/reporting/metrics/mute-total-duration.md)을 참조하세요.*

>[!ENDSHADEBOX]

음소거 플레이어 상태는 뷰어가 오디오를 음소거하고 음소거를 해제할 때 추적됩니다. 뷰어가 뮤트할 때 상태 시작 이벤트를 실행하고 뷰어가 뮤트할 때 상태 종료 이벤트를 실행합니다. 백엔드는 이러한 이벤트에서 영향을 받은 스트림, 상태 항목의 수 및 총 상태 시간 등 세 가지 지표를 계산합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.states.mute.set`, `a.media.states.mute.count`, `a.media.states.mute.time` |
| **XDM 컬렉션 필드** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) 및 [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details)&#x200B;(`name: "mute"`이(가) 있는 항목) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.states.mute.set`, `c_contextdata.a.media.states.mute.count`, `c_contextdata.a.media.states.mute.time` |
| **필수** | 아니요 |
| **전송 시점** | [상태 시작](/help/implementation/events/player-state/state-start.md), [상태 끝](/help/implementation/events/player-state/state-end.md) |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 사용하여 상태가 `statesStart`에 추가된 `media.statesUpdate` 이벤트를 보냅니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

뷰어가 음소거를 해제하면 `statesEnd`의 상태로 다른 이벤트를 보냅니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

`MediaConstants.PlayerState.MUTE` 상수와 함께 `tracker.trackPlayerStateStart()` 및 `tracker.trackPlayerStateEnd()`을(를) 사용합니다.

**iOS(Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android(Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.MUTE)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

## Roku(BrightScript)

`sendMediaEvent`을(를) 사용하여 상태가 `statesStart`에 추가된 `media.statesUpdate` 이벤트를 보냅니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "mute" }],
            "playhead": 60
        }
    }
})
```

뷰어가 음소거를 해제하면 `statesEnd`의 상태로 다른 이벤트를 보냅니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "mute" }],
            "playhead": 90
        }
    }
})
```

## Media Edge API

`statesStart`에서 `mute`(또는 뷰어가 음소거 해제할 때 `statesEnd`)로 [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "mute" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.createStateObject` 및 `ADB.Media.PlayerState.Mute` 상수 사용:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## Media Collection API

뷰어가 음소거하면 `stateStart` POST 요청을 보내고 음소거를 해제하면 `stateEnd` POST를 보냅니다.

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
