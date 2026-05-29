---
title: 비트율 변경
description: 플레이어가 다른 비트율로 전환할 때마다 비트율 변경 이벤트를 실행합니다.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 6%

---


# 비트율 변경

>[!BEGINSHADEBOX]

*이 페이지에서는 비트율 변경 이벤트를 구현하는 방법에 대해 설명합니다. 해당 보고 변수에 대해서는 [[!UICONTROL 비트율 변경] (차원)](/help/reporting/dimensions/bitrate-changes.md) 및 [[!UICONTROL 비트율 변경] (지표)](/help/reporting/metrics/bitrate-changes.md)을 참조하십시오.*

>[!ENDSHADEBOX]

비트율 변경 이벤트는 플레이어가 다른 비트율로 전환했음을 알립니다. 먼저 QoE 개체에서 [Bitrate](/help/implementation/variables/quality/bitrate.md) 값을 업데이트한 다음 비트율 변경 이벤트를 실행합니다. 백엔드는 이러한 이벤트의 수를 사용하여 [[!UICONTROL 비트율 변경]](/help/reporting/dimensions/bitrate-changes.md) 차원과 [[!UICONTROL 비트율 변경]](/help/reporting/metrics/bitrate-changes.md) 지표와 결과 비트율 값 피드 [[!UICONTROL 평균 비트율]](/help/reporting/metrics/average-bitrate.md)을 계산합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | (없음 — 백엔드에서 계산) |
| **XDM 이벤트 유형** | `media.bitrateChange` |
| **Audience Manager 트레이트** | `c_contextdata.a.media.qoe.bitrateChangeCount` |
| **필수** | 아니요 |
| **전송 시점** | [비트율 변경](/help/implementation/events/playback/bitrate-change.md) |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 사용하여 새 비트율로 `media.bitrateChange` 이벤트를 보냅니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 4500,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 120
    }
  }
});
```

>[!TAB iOS]

새 비트율로 QoE 개체를 업데이트한 다음 비트율 변경 이벤트를 실행합니다.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

새 비트율로 QoE 개체를 업데이트한 다음 비트율 변경 이벤트를 실행합니다.

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku]

`media.bitrateChange`과(와) 함께 `sendMediaEvent`을(를) 사용하여 비트율 변경을 신호로 보냅니다. `qoeDataDetails`에 새 비트율 포함:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 4500,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 120
        }
    }
})
```

>[!TAB 미디어 Edge API]

업데이트된 `qoeDataDetails`을(를) 사용하여 [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 4500
        },
        "sessionID": "{sid}",
        "playhead": 120
      }
    }
  }]
}
```

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

QoE 개체를 업데이트하고 이벤트를 실행합니다.

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB Chromecast]

새 비트율로 QoS 개체를 업데이트한 다음 비트율 변경 이벤트를 실행합니다.

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  4500,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB 미디어 컬렉션 API]

새 비트율을 사용하여 `bitrateChange` POST 요청 보내기:

```json
{
  "playerTime": { "playhead": 120, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 4500
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.

>[!ENDTABS]
