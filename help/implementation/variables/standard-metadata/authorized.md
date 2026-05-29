---
title: 인증됨
description: 승인된 이벤트로 카운트되도록 Adobe Pass을 통해 인증된 것으로 세션에 플래그를 지정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 9%

---


# 인증됨

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**Authorized**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 지표에 대해서는 [승인](/help/reporting/metrics/authorized.md)을 참조하십시오.*

>[!ENDSHADEBOX]

승인된 변수는 사용자가 Adobe Pass / TV-Everywhere를 통해 승인된 세션에 플래그를 지정합니다. 인증이 확인되면 `"TRUE"`(으)로 설정하십시오. 그렇지 않으면 설정하지 마십시오. [MVPD](/help/implementation/variables/standard-metadata/mvpd.md)와(과) 연결하여 공급자별 인증을 제거하십시오.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.pass.auth` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.pass.auth` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.sessionDetails` 내에서 `authorized`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        authorized: "TRUE"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

HashMap 인수에 메타데이터 키로 승인된 플래그를 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.AUTHORIZED` 사용.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

HashMap 인수에 메타데이터 키로 승인된 플래그를 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.AUTHORIZED` 사용.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `authorized`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "authorized": "TRUE"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.sessionDetails` 내의 `authorized`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "authorized": "TRUE"
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

`ADB.Media.VideoMetadataKeys.Authorized`을(를) 사용하여 `contextData` 개체에 승인된 플래그를 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Authorized] = "TRUE";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`trackSessionStart`을(를) 호출하기 전에 `ADBMobile.media.VideoMetadataKeys.AUTHORIZED`을(를) 사용하여 미디어 개체의 `StandardMediaMetadata` 속성에 승인된 플래그를 설정합니다.

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.AUTHORIZED] = "TRUE";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 미디어 컬렉션 API]

`params` 개체에 `media.pass.auth` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.auth": "TRUE"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.

>[!ENDTABS]
