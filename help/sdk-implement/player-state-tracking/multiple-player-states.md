---
title: 한 번에 여러 플레이어 상태 업데이트
description: 이 항목에서는 여러 플레이어 상태 추적 기능에 대해 설명합니다.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 7a28674024739593431a942d5e0a498294bbe793
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 10%

---

# 여러 플레이어 상태 추적

두 플레이어 상태가 동시에 시작하고 끝나는 상황 또는 상태 끝도 다른 상태의 시작인 경우가 있습니다. 다음 예를 봅니다.

![여러 플레이어 상태](assets/multiple-player-states.svg)

현재 구현에서는 두 시나리오를 허용합니다.
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

그러나 고객은 많은 문제를 해결해야 합니다 `stateStart` 및 `stateEnd` 여러 동시 상태 변경을 알리는 이벤트 이러한 일반적인 동작을 최적화하려면 `statesUpdate` 상태 목록을 종료하고 새 상태 목록을 시작하는 이벤트 유형이 구현되었습니다.

새로운 `statesUpdate` 이벤트를 발생시키면 위의 이벤트 목록이 다음과 같이 됩니다.
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

동일한 동작에 대해 상태 업데이트 호출 수가 6개에서 3개로 줄었습니다. 마지막 행사는 단순한 것일 수도 있다 `stateEnd(fullScreen)`.

## Media Collection API 구현

예:

```
// statesUpdate (ex: mute and pictureInPicture are switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: mute and pictureInPicture are switched off, fullScreen is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ],
    "statesStart": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: fullScreen is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

## Media SDK 구현

Media SDK 구현이 없습니다.
