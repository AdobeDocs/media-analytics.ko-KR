---
title: 에피소드
description: 개별 에피소드를 개별적으로 보고할 수 있도록 에피소드 콘텐츠에 대한 에피소드 번호를 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 16%

---


# 에피소드

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**Episode**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [에피소드](/help/reporting/dimensions/episode.md)를 참조하십시오.*

>[!ENDSHADEBOX]

에피소드 변수는 시즌 내 에피소드 번호입니다(일반적으로 `"13"`과(와) 같은 문자열 정수). 개별 에피소드별로 참여를 나눌 수 있도록 [Show](/help/implementation/variables/standard-metadata/show.md) 및 [Season](/help/implementation/variables/standard-metadata/season.md)과(와) 짝을 이룹니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.episode` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **필수** | 아니요 |
| **전송 시점** | 세션 시작, 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `episode`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        episode: "13"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

에피소드 번호를 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.EPISODE` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku(BrightScript)

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `episode`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "episode": "13"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails` 내의 `episode`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "episode": "13"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.VideoMetadataKeys.Episode`을(를) 사용하여 `contextData` 개체에 에피소드를 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "13";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`params` 개체에 `media.episode` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.episode": "13"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
