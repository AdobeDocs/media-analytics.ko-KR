---
title: 작성자
description: 콘텐츠 작성자를 설정합니다. 오디오북에 주로 사용됩니다.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 10%

---


# 작성자

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**작성자**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대해서는 [작성자](/help/reporting/dimensions/author.md)를 참조하십시오.*

>[!ENDSHADEBOX]

작성자 변수는 콘텐츠 작성자입니다(예: `"Eleanor Clementine"`). 오디오북에 주로 사용되지만 관련 속성이 호스트나 제작자인 팟캐스트에 대해서도 허용됩니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.author` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.author` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.sessionDetails` 내에서 `author`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        author: "Eleanor Clementine"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

작성자를 HashMap 인수에 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.AudioMetadataKeys.AUTHOR` 사용.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

작성자를 HashMap 인수에 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.AudioMetadataKeys.AUTHOR` 사용.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `author`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "author": "Eleanor Clementine"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.sessionDetails` 내의 `author`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "author": "Eleanor Clementine"
        },
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`ADB.Media.AudioMetadataKeys.Author`을(를) 사용하여 `contextData` 개체에 작성자를 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Author] = "Eleanor Clementine";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`trackSessionStart`을(를) 호출하기 전에 `ADBMobile.media.AudioMetadataKeys.AUTHOR`을(를) 사용하여 미디어 개체의 `StandardMediaMetadata` 속성에서 작성자를 설정하십시오.

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 미디어 컬렉션 API]

`params` 개체에 `media.author` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.author": "Eleanor Clementine"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.

>[!ENDTABS]
