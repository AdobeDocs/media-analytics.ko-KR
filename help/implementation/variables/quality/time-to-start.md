---
title: 시작 시간
description: 백엔드가 time-to-first-frame 품질을 보고할 수 있도록 플레이어의 시작 시간(밀리초)을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 9%

---


# 시작 시간

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**시작 시간**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원 및 지표에 대해서는 [시작 시간](/help/reporting/dimensions/time-to-start.md)을 참조하세요.*

>[!ENDSHADEBOX]

시작 시간 변수는 재생을 시작하는 플레이어와 첫 번째 프레임 렌더링 사이의 경과 시간(밀리초)입니다. 세션 시작 이벤트가 실행되기 전에 QoE 개체에서 설정하십시오. Adobe은 값을 초 단위로 저장하고 보고합니다. 전달 밀리초와 Adobe은 수집 시 전환됩니다.

>[!IMPORTANT]
>
>플레이어에서 콘텐츠 프레임 렌더링을 시작하면 `timeToStart` 업데이트를 중지합니다. 이 값은 초기 버퍼링 또는 로드 단계 동안 증가할 수 있지만 재생이 시작되는 순간부터 고정된 것으로 처리해야 합니다. 첫 번째 프레임 렌더링 후에도 계속 업데이트하면 부풀려지거나 잘못된 [시작 시간](/help/reporting/metrics/time-to-start.md) 지표가 생성됩니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.qoe.timeToStart` |
| **XDM 컬렉션 필드** | [`mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.qoe.timeToStart` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `media.sessionStart`의 `mediaCollection.qoeDataDetails` 내에서 `timeToStart`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      qoeDataDetails: {
        timeToStart: 30000
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

시작 시간을 두 번째 인수(`startupTime`)로 `createQoEObject`에 전달합니다.

**iOS(Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android(Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku(BrightScript)

`createMediaSession`을(를) 호출할 때 `media.sessionStart`의 `mediaCollection.qoeDataDetails` 내에서 `timeToStart`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "qoeDataDetails": {
                "timeToStart": 30000
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.qoeDataDetails` 내의 `timeToStart`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports"
        },
        "qoeDataDetails": {
          "timeToStart": 30000
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.createQoEObject`에 두 번째 인수로 시작할 시간을 전달합니다.

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

## Media Collection API

`sessionStart`의 `params` 개체에 `media.qoe.timeToStart` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.qoe.timeToStart": 30000
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
