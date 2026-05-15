---
title: 비트율
description: 백엔드가 비트율 지표를 계산할 수 있도록 QoE 개체에서 현재 재생 비트율(kbps)을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 10%

---


# 비트율

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**Bitrate**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 변수에 대해서는 [평균 비트 전송률(차원)](/help/reporting/dimensions/average-bitrate.md) 및 [평균 비트 전송률(지표)](/help/reporting/metrics/average-bitrate.md)을 참조하십시오.*

>[!ENDSHADEBOX]

bitrate 변수는 현재 재생 비트율입니다(초당 킬로비트). 플레이어가 비트율을 협상할 때마다 QoE 개체에 설정하고 비트율이 변경되면 QoE 개체를 업데이트합니다. 백엔드는 비트율 값을 사용하여 평균 비트율, 비트율 버킷당 차원 및 비트율 변경 지표를 계산합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.qoe.bitrateAverageBucket` |
| **XDM 컬렉션 필드** | [`mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.qoe.bitrateAverageBucket` |
| **필수** | 아니요 |
| **전송 시점** | 품질 이벤트([비트율 변경](/help/implementation/events/playback/bitrate-change.md), [버퍼 시작](/help/implementation/events/playback/buffer-start.md), [오류](/help/implementation/events/error.md)), 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `media.bitrateChange`(또는 품질 관련 이벤트)의 `mediaCollection.qoeDataDetails` 내에서 `bitrate`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

비트율을 첫 번째 인수로 `createQoEObject`에 전달합니다. 품질 이벤트가 실행되기 전에 추적기에서 QoE 개체를 업데이트합니다.

**iOS(Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android(Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku(BrightScript)

`media.bitrateChange`과(와) 같은 품질 이벤트에 대해 `sendMediaEvent`을(를) 호출할 때 `mediaCollection.qoeDataDetails` 내에서 `bitrate`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

## Media Edge API

`mediaCollection.qoeDataDetails` 내의 `bitrate`을(를) 사용하여 [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Media SDK

비트율을 첫 번째 인수로 `ADB.Media.createQoEObject`에 전달하고 추적기를 업데이트하십시오.

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
```

## Media Collection API

`bitrateChange` POST 요청의 `params` 개체에 `media.qoe.bitrate` 포함:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 3200
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
