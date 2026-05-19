---
title: 비트율 변경
description: 재생 비트율이 변경되었음을 나타냅니다.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 14%

---


# 비트율 변경

비트율 변경 이벤트는 플레이어가 새 재생 비트율을 협상했음을 알립니다. 재생 중에 비트율이 변경될 때마다 전송합니다. 백엔드가 [평균 비트율](/help/reporting/metrics/average-bitrate.md) 및 비트율 버킷당 차원을 계산할 수 있도록 QoE 데이터에 새 비트율 값을 포함하십시오.

* **필수 구성 요소**: [세션 시작](../session/session-start.md)
* **관련 지표**: [비트율 변경](/help/reporting/metrics/bitrate-changes.md)

## Web SDK

`eventType: "media.bitrateChange"` 및 `qoeDataDetails`의 새 비트 전송률로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출합니다.

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

새 비트율로 QoE 개체를 만들고 비트율 변경 이벤트가 실행되기 전에 추적기를 업데이트합니다.

**iOS(Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android(Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200, 0, 24, 0)

tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku(BrightScript)

`eventType: "media.bitrateChange"` 및 `qoeDataDetails`의 새 비트율로 `sendMediaEvent`을(를) 호출합니다.

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

`qoeDataDetails`에서 새 비트율을 사용하여 [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/) 끝점을 호출합니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bitrateChange?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

새 비트율로 QoE 개체를 만들고 추적기를 업데이트합니다.

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## Media Collection API

`qoeData`에서 새 비트율을 사용하여 [이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `bitrateChange` POST를 보냅니다.

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "qoeData": {
    "media.qoe.bitrate": 3200
  }
}
```
