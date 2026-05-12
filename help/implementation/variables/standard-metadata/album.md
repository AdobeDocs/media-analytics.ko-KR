---
title: 앨범
description: 오디오 콘텐츠의 앨범 이름을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 17%

---


# 앨범

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**앨범**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [앨범](/help/reporting/dimensions/album.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

Album 변수는 오디오 트랙이 속한 앨범의 이름입니다(예: `"Pinegrove"`). 이 링크를 사용하여 동일한 앨범의 트랙에 걸쳐 참여를 롤업할 수 있습니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.album` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.album`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-collection) |
| **필수** | 아니요 |
| **전송 시점** | 세션 시작, 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `album`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        album: "Pinegrove"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

앨범을 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.AudioMetadataKeys.ALBUM` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.ALBUM] = "Pinegrove"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.ALBUM] = "Pinegrove"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku(BrightScript)

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `album`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "album": "Pinegrove"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails` 내의 `album`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "album": "Pinegrove"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.AudioMetadataKeys.Album`을(를) 사용하여 `contextData` 개체에 앨범을 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Album] = "Pinegrove";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`params` 개체에 `media.album` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.album": "Pinegrove"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
