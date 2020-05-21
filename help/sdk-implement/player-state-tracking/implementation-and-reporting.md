---
title: 구현 및 보고
description: 이 항목에서는 다음을 포함한 플레이어 상태 추적 기능을 구현하는 방법에 대해 설명합니다.
translation-type: tm+mt
source-git-commit: b0bfe74d1f6083e700dbf98f504a17518bd19ecb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 구현 및 보고

재생 세션 중에 각 상태 발생(처음부터 끝까지)을 개별적으로 추적해야 합니다. Media SDK 및 Media Collection API는 이 기능에 대한 새로운 추적 방법을 제공합니다.

Media SDK에는 사용자 지정 상태 추적을 위한 두 가지 새로운 방법이 포함되어 있습니다.

`trackStateStart("state_name")`

`trackStateClose("state_name")`


Media Collection API에는 &quot;media.stateName&quot;을 필수 매개 변수로 사용하는 두 개의 새로운 이벤트가 포함되어 있습니다.

`stateStart` 및 `stateEnd`

## 미디어 SDK 구현

플레이어 상태 시작

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

플레이어 상태 종료

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## Media Collection API 구현

플레이어 상태 시작

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

플레이어 상태 종료

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## 상태 지표

각 개별 상태에 대해 제공된 지표가 계산되고 컨텍스트 데이터 매개 변수로 Adobe Analytics에 푸시되어 보고용으로 저장됩니다. 각 주에 대해 세 개의 지표를 사용할 수 있습니다.

* `a.media.states.(media.state.name).set = true` — 스트림의 각 특정 재생에 대해 상태가 최소 한 번 설정되면 true로 설정됩니다.
* `a.media.states.(media.state.name).count = 4` — 스트림의 각 개별 재생 동안 상태 발생 횟수를 식별합니다
* `a.media.states.(media.state.name).time = 240` — 스트림의 개별 재생당 총 상태 지속 시간(초)을 식별합니다

## 보고

모든 상태 지표는 보고 시각화 또는 구성 요소(세그먼트, 계산된 지표)에 사용할 수 있습니다.
TBD - 소스/wiki에서 업데이트된 정보 확인 - AW의 스크린샷

## Adobe Experience Platform으로 플레이어 명시된 지표 가져오기

Analytics에 저장된 데이터는 어떤 목적으로든 사용할 수 있으며, 플레이어 상태 지표는 XDM을 사용하여 Adobe Experience Platform으로 가져와서 고객 경로 분석과 함께 사용할 수 있습니다. 표준 상태 속성에는 특정 속성이 있지만 사용자 지정 상태는 사용자 지정 이벤트를 통해 사용할 수 있습니다. 자세한 내용은 XDM ID 속성 목록(?LINK TO METRIC LIST? )을 참조하십시오.