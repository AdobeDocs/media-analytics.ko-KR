---
title: 세션 시작
description: 미디어 세션의 시작 신호를 보내고 모든 후속 이벤트에 필요한 세션 ID를 얻습니다.
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 10%

---


# 세션 시작

세션 시작 이벤트는 미디어 추적 세션을 엽니다. 재생에 대해 전송된 첫 번째 이벤트여야 합니다. 응답은 동일한 세션에 대한 모든 후속 이벤트에 포함되어야 하는 세션 ID를 반환합니다.

**10분 동안 이벤트가 수신되지 않았거나**, **30분 동안 플레이헤드 이동이 없으면** 세션이 자동으로 만료됩니다. 세션이 만료되면 세션 시작을 다시 호출하여 새 세션 ID를 얻어야 합니다.

* **필수 구성 요소**: 없음, 항상 첫 번째 이벤트
* **관련 지표**: [미디어 시작](/help/reporting/metrics/media-starts.md)

## Web SDK

`eventType: "media.sessionStart"` 및 필수 `sessionDetails`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출합니다. 응답에 `handle[].payload[].sessionId`(유형 `media-analytics:new-session`)의 세션 ID가 포함되어 있습니다. 이 값을 저장하고 모든 후속 이벤트에서 `sessionID`(으)로 전달하십시오.

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
      playhead: 0
    }
  }
});
```

## Mobile SDK

미디어 개체 및 선택적 메타데이터를 사용하여 `trackSessionStart`을(를) 호출합니다.

**iOS(Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android(Kotlin)**

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

## Roku(BrightScript)

필요한 세션 세부 정보로 `createMediaSession`을(를) 호출합니다.

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
            "playhead": 0
        }
    }
})
```

## Media Edge API

[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다. 응답에 `handle[].payload[].sessionId`(유형 `media-analytics:new-session`)의 세션 ID가 포함되어 있습니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "playerName": "HTML5 Player",
          "contentType": "VOD",
          "length": 128,
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}'
```

## Media SDK

`ADB.Media.createMediaObject`을(를) 사용하여 만든 미디어 개체로 `trackSessionStart`을(를) 호출합니다.

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123",                  // name
  "video-id-123",               // media ID
  128,                          // length (seconds)
  ADB.Media.StreamType.VOD,     // stream type
  ADB.Media.MediaType.Video     // media type
);

tracker.trackSessionStart(mediaObject, null);
```

## Media Collection API

[세션 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)에 `sessionStart` POST를 보냅니다. 응답 `Location` 헤더에 모든 후속 이벤트 요청에 사용할 세션 ID가 포함되어 있습니다.

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123"
  }
}
```
