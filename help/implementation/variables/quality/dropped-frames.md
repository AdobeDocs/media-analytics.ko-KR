---
title: 드롭된 프레임
description: 백엔드가 프레임 드롭 품질을 보고할 수 있도록 QoE 개체에서 드롭된 프레임의 실행 수를 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 9%

---


# 드롭된 프레임

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**삭제된 프레임**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원 및 지표에 대해서는 [삭제된 프레임](/help/reporting/dimensions/dropped-frames.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

드롭된 프레임 변수는 세션 중에 플레이어가 드롭한 프레임의 실행 횟수입니다. QoE 개체에 설정하고 플레이어가 새 드롭을 보고할 때마다 값을 업데이트합니다. 백엔드가 세션 종료 시 최신 값을 보고합니다.

>[!NOTE]
>
>간격 델타가 아닌 해당 시점까지 전체 세션에 대해 드롭된 프레임의 **누적 합계**&#x200B;를 항상 전달하십시오. 업데이트 사이에 값을 `0`(으)로 재설정하면 백엔드가 `0`을(를) 최종 값으로 수신하고 이전에 실제로 삭제한 내용과 관계없이 세션에 대해 0개의 삭제된 프레임을 보고합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.qoe.droppedFrameCount` |
| **XDM 컬렉션 필드** | [`mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.qoe.droppedFrameCount` |
| **필수** | 아니요 |
| **전송 시점** | 품질 이벤트([비트율 변경](/help/implementation/events/playback/bitrate-change.md), [버퍼 시작](/help/implementation/events/playback/buffer-start.md), [오류](/help/implementation/events/error.md)), 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.qoeDataDetails` 내에서 `droppedFrames`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 3
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

드롭된 프레임을 `createQoEObject`에 네 번째 인수로 전달합니다. 품질 이벤트가 실행되기 전에 추적기를 업데이트합니다.

**iOS(Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android(Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

## Roku(BrightScript)

`sendMediaEvent`을(를) 호출할 때 `mediaCollection.qoeDataDetails` 내에서 `droppedFrames`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 3
            },
            "playhead": 90
        }
    }
})
```

## Media Edge API

`mediaCollection.qoeDataDetails` 내의 `droppedFrames`을(를) 사용하여 [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "droppedFrames": 3
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Media SDK

드롭된 프레임을 `ADB.Media.createQoEObject`에 네 번째 인수로 전달:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

## Media Collection API

`params` 개체에 `media.qoe.droppedFrames` 포함:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.droppedFrames": 3
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
