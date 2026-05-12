---
title: 콘텐츠 다시 시작
description: 백엔드가 콘텐츠 다시 시작 이벤트를 계산하도록 이전에 중단된 재생을 다시 시작하는 세션에 플래그를 지정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 10%

---


# 콘텐츠 다시 시작

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**콘텐츠 다시 시작**변수에 대한 데이터 수집을 다룹니다. 해당 보고 지표에 대해서는 [콘텐츠 다시 시작](/help/reporting/metrics/content-resumes.md)을 참조하십시오.*

>[!ENDSHADEBOX]

콘텐츠는 이전에 중단된 재생을 재개하는 세션에 플래그를 지정합니다. 백엔드가 세션에 대한 콘텐츠 다시 시작 이벤트를 계산하고 새 스트림 계산에서 제외하도록 `media.sessionStart`에 설정합니다. 직접 API 및 Edge API 구현의 경우 클라이언트는 재개된 세션을 감지하고(예: 30분을 초과하는 버퍼, 일시 중지 또는 중지 후) 이 플래그를 적절하게 설정해야 합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.resume` |
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **필수** | 아니요 |
| **전송 시점** | 세션 시작 |

## Web SDK

다시 시작된 세션에 대해 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `hasResume`을(를) `mediaCollection.sessionDetails` 내의 `true`(으)로 설정합니다.

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
        streamType: "video",
        hasResume: true
      },
      playhead: 60
    }
  }
});
```

## Mobile SDK

`trackSessionStart`에서 다시 시작 플래그를 미디어 개체의 선택적 구성 번들의 일부로 전달합니다. `MediaConstants.MediaObjectKey.RESUMED` 키를 사용합니다.

**iOS(Swift)**

```swift
var mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)
mediaObject?[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android(Kotlin)**

```kotlin
val mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)
mediaInfo[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(mediaInfo, null)
```

## Roku(BrightScript)

다시 시작된 세션에 대해 `createMediaSession`을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `hasResume`을(를) `true`(으)로 설정합니다.

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
                "streamType": "video",
                "hasResume": true
            },
            "playhead": 60
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails` 내에서 `hasResume`이(가) `true`(으)로 설정된 상태에서 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "hasResume": true
        },
        "playhead": 60
      }
    }
  }]
}
```

## Media SDK

`trackSessionStart`을(를) 호출하기 전에 미디어 정보 개체에 `RESUMED` 키를 설정합니다.

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);
mediaInfo[ADB.Media.MediaObjectKey.Resumed] = true;

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

`sessionStart` POST 요청의 `params` 개체에 `media.resume` 포함:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.resume": true
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.
