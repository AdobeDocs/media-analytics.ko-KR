---
title: MVPD
description: 사용자가 Adobe Pass을 통해 인증하면 다중 채널 비디오 프로그래밍 배포자를 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 15%

---


# MVPD

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**MVPD**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대해서는 [MVPD](/help/reporting/dimensions/mvpd.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

MVPD(다중 채널 비디오 프로그래밍 배포자) 변수는 사용자가 인증한 케이블, 위성 또는 가상 MVPD 공급자(예: `"Comcast"`, `"DirecTV"` 또는 `"YouTubeTV"`)입니다. 콘텐츠가 Adobe Pass 또는 TV-Everywhere 인증 뒤에 게이팅될 때 설정합니다. 인증을 완료한 세션을 추적하려면 [Authorized](/help/implementation/variables/standard-metadata/authorized.md)와(과) 연결하십시오.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.pass.mvpd` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **필수** | 아니요 |
| **전송 시점** | 세션 시작, 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `mvpd`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        mvpd: "Comcast"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

HashMap 인수에 메타데이터 키로 MVPD을 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.MVPD` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku(BrightScript)

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `mvpd`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "mvpd": "Comcast"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails` 내의 `mvpd`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "channel": "Sports",
          "mvpd": "Comcast"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.VideoMetadataKeys.MVPD`을(를) 사용하여 `contextData` 개체에 MVPD 전달:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.MVPD] = "Comcast";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`params` 개체에 `media.pass.mvpd` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.mvpd": "Comcast"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
