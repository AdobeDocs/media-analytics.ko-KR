---
title: 표시
description: 에피소드가 보고에서 단일 프로그램으로 롤업되도록 시리즈의 일부인 비디오 컨텐츠의 표시 이름을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 8%

---


# 표시

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**Show**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대해 [표시](/help/reporting/dimensions/show.md)를 참조하십시오.*

>[!ENDSHADEBOX]

show 변수는 프로그램 또는 시리즈 이름입니다(예: `"Blinding Light"` 또는 `"Coastline Mysteries"`). 콘텐츠가 시리즈에 속하는 모든 세션에 설정하여 여러 시즌의 에피소드가 표시 차원의 단일 라인 항목으로 롤업되도록 할 수 있습니다. 시리즈의 일부가 아닌 일회성 컨텐츠에 대해서는 설정하지 마십시오.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.show` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.show` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.sessionDetails` 내에서 `show`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        show: "Blinding Light"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

HashMap 인수에 표시 이름을 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.SHOW` 사용.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

HashMap 인수에 표시 이름을 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.SHOW` 사용.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `show`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "show": "Blinding Light"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.sessionDetails` 내의 `show`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "show": "Blinding Light"
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

`ADB.Media.VideoMetadataKeys.Show`을(를) 사용하여 `contextData` 개체에 표시 이름을 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Show] = "Blinding Light";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`trackSessionStart`을(를) 호출하기 전에 `ADBMobile.media.VideoMetadataKeys.SHOW`을(를) 사용하여 미디어 개체의 `StandardMediaMetadata` 속성에 표시 이름을 설정합니다.

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "Blinding Light";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 미디어 컬렉션 API]

`sessionStart` POST 요청의 `params` 개체에 `media.show` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.show": "Blinding Light"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.

>[!ENDTABS]
