---
title: 비트율 변경
description: 재생 비트율이 변경되었음을 나타냅니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 6%

---


# 비트율 변경

비트율 변경 이벤트는 플레이어가 새 재생 비트율을 협상했음을 알립니다. 재생 중에 비트율이 변경될 때마다 전송합니다. 백엔드가 [[!UICONTROL 평균 비트율]](/help/reporting/metrics/average-bitrate.md) 및 비트율 버킷당 차원을 계산할 수 있도록 QoE 데이터에 새 비트율 값을 포함하십시오.

* **필수 구성 요소**: [세션 시작](../session/session-start.md)
* **관련 지표**: [[!UICONTROL 비트율 변경]](/help/reporting/metrics/bitrate-changes.md)

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

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

>[!TAB iOS]

새 비트율로 QoE 개체를 만들고 비트율 변경 이벤트가 실행되기 전에 추적기를 업데이트합니다.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

새 비트율로 QoE 개체를 만들고 비트율 변경 이벤트가 실행되기 전에 추적기를 업데이트합니다.

```kotlin
val qoeObject = Media.createQoEObject(3200, 0, 24, 0)

tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB 미디어 Edge API]

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

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

`getQoSObject` 대리자가 반환한 QoS 개체를 업데이트한 다음 이벤트를 추적합니다.

```javascript
// Update QoS data via the delegate
this._qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // dropped frames
  24,    // fps
  0      // startup time
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB Roku 2.x]

`adb_media_init_qosinfo`을(를) 사용하여 새 비트율로 QoS 개체를 만들고 `mediaUpdateQoS`(으)로 추적기를 업데이트한 다음 이벤트를 추적합니다. Roku 매개 변수 순서: `bitrate, startupTime, fps, droppedFrames`을(를) 참고하십시오.

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
adb.mediaTrackEvent(adb.MEDIA_BITRATE_CHANGE)
```

>[!TAB 미디어 컬렉션 API]

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

>[!ENDTABS]
