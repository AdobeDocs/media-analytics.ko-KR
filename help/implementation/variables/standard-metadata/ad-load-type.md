---
title: 광고 로드 유형
description: 스트리밍 세션에 대한 광고 로드 유형을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 3%

---


# 광고 로드 유형

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**광고 로드 형식**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [광고 로드](/help/reporting/dimensions/ad-load-type.md)를 참조하십시오.*

>[!ENDSHADEBOX]

광고 로드 유형 변수는 세션 시작 시 로드되는 광고 유형을 식별합니다. 이 값은 조직의 내부 광고 게재 시스템에 의해 정의되며 표준 열거형으로 제한되지 않습니다. `"linear"`, `"dynamic"` 또는 `"programmatic"`과 같이 구현에 의미 있는 문자열을 사용할 수 있습니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.adLoad` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.adLoad` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`createMediaSession`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/createmediasession)을(를) 호출할 때 `xdm.mediaCollection.sessionDetails` 내에서 `adLoad`을(를) 설정합니다.

```javascript
alloy("createMediaSession", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
        length: 300,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        adLoad: "linear"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

광고 로드 형식을 사전 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.AD_LOAD` 사용.

```swift
var videoMetadata: [String: String] = [:]
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(info: mediaObject, metadata: videoMetadata)
```

>[!TAB Android]

광고 로드 형식을 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.AD_LOAD` 사용.

```kotlin
val videoMetadata = HashMap<String, String>()
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(mediaInfo, videoMetadata)
```

>[!TAB Roku]

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `adLoad`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "adLoad": "linear"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.sessionDetails` 내의 `adLoad`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "adLoad": "linear"
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

`ADB.Media.VideoMetadataKeys.AdLoad`을(를) 사용하여 `contextData` 개체에 광고 로드 유형을 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AdLoad] = "linear";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`trackSessionStart`을(를) 호출하기 전에 `ADBMobile.media.VideoMetadataKeys.AD_LOAD`을(를) 사용하여 미디어 개체의 `StandardMediaMetadata` 속성에서 광고 로드 유형을 설정하십시오.

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 300,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "linear";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 미디어 컬렉션 API]

`sessionStart` POST 요청의 `params` 개체에 `media.adLoad` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.adLoad": "linear"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.

>[!ENDTABS]
