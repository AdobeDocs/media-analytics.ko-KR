---
title: 레이블
description: 오디오 콘텐츠를 릴리스한 레코드 레이블을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 10%

---


# 레이블

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**Label**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [레이블](/help/reporting/dimensions/label.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

레이블 변수는 오디오 콘텐츠를 릴리스한 레코드 레이블의 이름입니다(예: `"Capitol Records"`). 음악 또는 팟캐스트 카탈로그의 레이블에 대한 참여를 비교할 때 사용합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.label` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.sessionDetails.label`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.label` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.sessionDetails` 내에서 `label`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        label: "Capitol Records"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

레이블을 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.AudioMetadataKeys.LABEL` 사용.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.LABEL] = "Capitol Records"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

레이블을 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.AudioMetadataKeys.LABEL` 사용.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.LABEL] = "Capitol Records"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `label`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "label": "Capitol Records"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.sessionDetails` 내의 `label`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "label": "Capitol Records"
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

`ADB.Media.AudioMetadataKeys.Label`을(를) 사용하여 `contextData` 개체에 레이블을 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Label] = "Capitol Records";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`trackSessionStart`을(를) 호출하기 전에 `ADBMobile.media.AudioMetadataKeys.LABEL`을(를) 사용하여 미디어 개체의 `StandardMediaMetadata` 속성에 레코드 레이블을 설정합니다.

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.LABEL] = "Capitol Records";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 미디어 컬렉션 API]

`params` 개체에 `media.label` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.label": "Capitol Records"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.

>[!ENDTABS]
