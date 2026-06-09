---
title: 스트림 형식
description: 스트림 형식을 설정하여 품질 계층(HD, SD 또는 게재 파이프라인에서 사용하는 다른 레이블)을 식별합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 7%

---


# 스트림 형식

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**스트림 형식**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [스트림 형식](/help/reporting/dimensions/stream-format.md)을 참조하세요.*

>[!ENDSHADEBOX]

스트림 형식 변수는 스트림의 품질 계층을 식별합니다(일반적으로 `"HD"` 또는 `"SD"`이지만 모든 문자열이 허용됨). 게재 품질 계층별로 참여, 완료 또는 품질을 분석하려는 경우 설정합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.format` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.sessionDetails.streamFormat`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.format` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.sessionDetails` 내에서 `streamFormat`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        streamFormat: "HD"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

스트림 형식을 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.STREAM_FORMAT` 사용.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

스트림 형식을 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.STREAM_FORMAT` 사용.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `streamFormat`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "streamFormat": "HD"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.sessionDetails` 내의 `streamFormat`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "streamFormat": "HD"
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

`ADB.Media.VideoMetadataKeys.StreamFormat`을(를) 사용하여 `contextData` 개체에 스트림 형식을 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.StreamFormat] = "HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`trackSessionStart`을(를) 호출하기 전에 `ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT`을(를) 사용하여 미디어 개체의 `StandardMediaMetadata` 속성에서 스트림 형식을 설정하십시오.

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT] = "HD";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

`mediaTrackSessionStart`을(를) 호출하기 전에 `MEDIA_VideoMetadataKeySTREAM_FORMAT`을(를) 사용하여 미디어 개체의 표준 메타데이터에서 스트림 형식을 설정하십시오.

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeySTREAM_FORMAT] = "HD"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 미디어 컬렉션 API]

`sessionStart` POST 요청의 `params` 개체에 `media.streamFormat` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamFormat": "HD"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.

>[!ENDTABS]
