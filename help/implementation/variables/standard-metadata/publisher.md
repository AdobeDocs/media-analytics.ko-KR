---
title: 게시자
description: 오디오 콘텐츠 게시자를 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 16%

---


# 게시자

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**게시자**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대해서는 [게시자](/help/reporting/dimensions/publisher.md)를 참조하십시오.*

>[!ENDSHADEBOX]

게시자 변수는 오디오 콘텐츠 게시자(예: 팟캐스트 네트워크 또는 오디오북 게시자)의 이름입니다. 이를 사용하여 조정된 오디오 카탈로그의 게시자 간 참여를 비교할 수 있습니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.publisher` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **필수** | 아니요 |
| **전송 시점** | 세션 시작, 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `publisher`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        publisher: "Northbridge Audio"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

게시자를 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.AudioMetadataKeys.PUBLISHER` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku(BrightScript)

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `publisher`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "publisher": "Northbridge Audio"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails` 내의 `publisher`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "publisher": "Northbridge Audio"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.AudioMetadataKeys.Publisher`을(를) 사용하여 `contextData` 개체에 게시자를 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Publisher] = "Northbridge Audio";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`params` 개체에 `media.publisher` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.publisher": "Northbridge Audio"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
