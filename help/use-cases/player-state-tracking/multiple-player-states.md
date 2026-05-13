---
title: 한 번에 여러 플레이어 상태 업데이트
description: 이 항목에서는 여러 플레이어 상태 추적 기능에 대해 설명합니다.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 7a512a81-a6d1-4d0c-a4fe-91e9b11419db
TQID: https://experienceleague.adobe.com/fKpr-TULVqDnK7j07e66gd-kiFLYzf7D2GmoGtP8Aqg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 186
ht-degree: 80%

---

# 여러 플레이어 상태 추적

때로는 두 플레이어 상태가 동시에 시작되고 끝나거나 다음 이미지와 같이 상태의 끝이 다른 상태의 시작일 수 도 합니다.

![여러 플레이어 상태](assets/multiple-player-states.png)

현재 구현에서는 두 가지 시나리오를 모두 허용합니다.
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

그러나 이를 위해서는 여러 `stateStart` 및 `stateEnd` 이벤트를 발행하여 여러 동시 상태 변경 신호를 보내야 합니다. 위치
이 일반적인 동작을 최적화하기 위해 상태 목록을 종료하는 새 `statesUpdate` 이벤트 유형이 구현되었습니다.
새 상태 목록을 시작합니다.

새로운 `statesUpdate` 이벤트를 사용하면 위의 이벤트 목록이 다음과 같이 됩니다.
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

동일한 동작에 대해 상태 업데이트 호출 수가 6개에서 3개로 줄었습니다. 마지막 이벤트
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
