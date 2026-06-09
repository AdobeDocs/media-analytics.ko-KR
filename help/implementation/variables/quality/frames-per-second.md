---
title: 초당 프레임
description: 백엔드에 품질 보고를 위한 프레임 속도 컨텍스트가 있도록 QoE 개체에 대한 현재 프레임 속도를 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 7%

---


# 초당 프레임

초당 프레임 수 변수는 스트림의 현재 프레임 속도입니다. 백엔드가 각 재생 세션에 대한 전체 품질 컨텍스트를 갖도록 비트율 및 드롭된 프레임과 함께 QoE 개체에 설정합니다. Adobe Analytics은 프레임 속도에 대한 보고 변수를 자동으로 만들지 않습니다. 보고서로 표시하려는 경우 사용자 지정 처리 규칙을 만듭니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | 없음(Adobe Analytics에서 프레임 속도에 대해 예약된 컨텍스트 데이터 키를 할당하지 않음) |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.qoeDataDetails.framesPerSecond`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager 트레이트** | 해당 사항 없음 |
| **필수** | 아니요 |
| **전송 시점** | 품질 이벤트([비트율 변경](/help/implementation/events/playback/bitrate-change.md), [버퍼 시작](/help/implementation/events/playback/buffer-start.md), [오류](/help/implementation/events/error.md)), 세션 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.qoeDataDetails` 내에서 `framesPerSecond`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        framesPerSecond: 24
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

프레임 속도를 세 번째 인수(`fps`)로 `createQoEObject`에 전달합니다.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

프레임 속도를 세 번째 인수(`fps`)로 `createQoEObject`에 전달합니다.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

`sendMediaEvent`을(를) 호출할 때 `xdm.mediaCollection.qoeDataDetails` 내에서 `framesPerSecond`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "framesPerSecond": 24
            },
            "playhead": 90
        }
    }
})
```

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.qoeDataDetails` 내의 `framesPerSecond`을(를) 사용하여 [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "framesPerSecond": 24
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

프레임 속도를 세 번째 인수로 `ADB.Media.createQoEObject`에 전달합니다.

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

프레임 속도를 세 번째 인수(`fps`)로 `ADBMobile.media.createQoSObject`에 전달하고 추적기를 업데이트합니다.

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

프레임 속도를 세 번째 인수(`fps`)로 `adb_media_init_qosinfo`에 전달하고 `mediaUpdateQoS`(으)로 추적기를 업데이트하십시오.

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB 미디어 컬렉션 API]

`params` 개체에 `media.qoe.framesPerSecond` 포함:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.framesPerSecond": 24
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.

>[!ENDTABS]
