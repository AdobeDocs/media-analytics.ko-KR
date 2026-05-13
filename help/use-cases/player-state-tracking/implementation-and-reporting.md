---
title: 구현 및 보고
description: 다음을 포함한 플레이어 상태 추적 기능을 구현하는 방법에 대해 알아봅니다.
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/NzekVHZYctiEjAWDpRhIdiw74amAX3wTX-z2nZDgvIw
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
  - id: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 308
ht-degree: 76%

---

# 구현 및 보고

재생 세션 중에 각 상태 발생(처음부터 끝까지)을 개별적으로 추적해야 합니다. Media SDK 및 Media Collection API는 이 기능에 대한 추적 메서드를 제공합니다.

Media SDK에는 사용자 지정 상태 추적을 위한 두 가지 방법이 포함됩니다.

`trackStateStart("state_name")`

`trackStateClose("state_name")`


Media Collection API에는 `media.stateName`을(를) 필수 매개 변수로 사용하는 두 개의 이벤트가 포함되어 있습니다.

`stateStart` 및 `stateEnd`

## Media SDK 구현

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

각 개별 상태에 대해 제공된 지표가 계산되고 컨텍스트 데이터 매개 변수로 Adobe Analytics에 푸시되어 보고용으로 저장됩니다. 각 상태에 대해 세 개의 지표를 사용할 수 있습니다.

* `a.media.states.[state.name].set = true` — 스트림의 각 특정 재생에 대해 상태가 최소 한 번 이상 설정되면 true로 설정합니다.
* `a.media.states.[state.name].count = 4` — 스트림의 각 개별 재생 동안 상태 발생 횟수를 식별합니다.
* `a.media.states.[state.name].time = 240` — 스트림의 각 개별 재생당 총 상태 지속 시간(초)을 식별합니다.

## 보고

플레이어 상태 추적을 위해 보고서 세트를 활성화하면 Analysis Workspace 또는 구성 요소(세그먼트, 계산된 지표)에서 사용할 수 있는 모든 보고 시각화에 모든 플레이어 상태 지표를 사용할 수 있습니다. 이러한 지표는 미디어 보고 설정(설정 편집 > 미디어 관리 > 미디어 보고)을 사용하는 각 개별 보고서에 대해 Admin Console에서 활성화할 수 있습니다.

![](assets/report-setup.png)

Analysis Workspace에서 새 속성은 모두 지표 패널에 있습니다. 예를 들어 `full screen`별로 검색하여 지표 패널에서 전체 화면 데이터를 볼 수 있습니다.

![](assets/full-screen-report.png)

## Adobe Experience Platform으로 플레이어에서 명시한 지표 가져오기

Analytics에 저장된 데이터는 어떤 목적으로든 사용할 수 있으며, 플레이어 상태 지표는 XDM을 사용하여 Adobe Experience Platform으로 가져와서 Customer Journey Analytics와 함께 사용할 수 있습니다. 표준 상태 속성에는 특정 속성이 있지만 사용자 지정 상태 속성은 사용자 지정 이벤트를 통해 사용할 수 있습니다.
