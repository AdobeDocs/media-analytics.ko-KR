---
title: 한 번에 여러 플레이어 상태 업데이트
description: 이 항목에서는 여러 플레이어 상태 추적 기능에 대해 설명합니다.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: fdbb777547181422b81ff6f7874bec3d317d02e9
workflow-type: ht
source-wordcount: '186'
ht-degree: 100%

---

# 여러 플레이어 상태 추적

때로는 두 플레이어 상태가 동시에 시작되고 끝나거나 다음 이미지와 같이 상태의 끝이 다른 상태의 시작일 수 도 합니다.

![여러 플레이어 상태](assets/multiple-player-states.svg)

현재 구현에서는 두 가지 시나리오를 모두 허용합니다.
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

그러나 이를 위해서는 여러 `stateStart` 및 `stateEnd` 이벤트를 발행하여 여러 동시 상태 변경 신호를 보내야 합니다. 이렇게 자주 사용되는 동작을 최적화하기 위해 상태 목록을 종료하고 새 상태 목록을 시작하는 새로운 `statesUpdate` 이벤트 유형이 구현되었습니다.

새로운 `statesUpdate` 이벤트를 사용하면 위의 이벤트 목록이 다음과 같이 됩니다.
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

동일한 동작에 대해 상태 업데이트 호출 수가 6개에서 3개로 줄었습니다. 마지막 이벤트는
단순한 `stateEnd(fullScreen)`일 수도 있습니다.

## Media Collection API 구현 {#mpst-api}

미디어 컬렉션 API를 사용하여 여러 플레이어 상태 추적을 구현할 수 있습니다.

### 예

다음은 여러 플레이어 상태 추적을 위한 미디어 컬렉션 API 구현 예를 보여 줍니다.

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

미디어 SDK 구현이 없습니다.
