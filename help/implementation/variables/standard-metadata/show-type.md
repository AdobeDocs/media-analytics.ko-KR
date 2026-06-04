---
title: 유형 표시
description: 문자열 정수 코드를 사용하여 콘텐츠 형식(전체 에피소드, 미리보기, 클립 또는 기타)을 식별합니다.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 8%

---


# 유형 표시

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**표시 형식**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [표시 형식](/help/reporting/dimensions/show-type.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

show type 변수는 문자열 정수 코드를 사용하여 콘텐츠 형식을 식별합니다.

* `"0"`: 전체 에피소드
* `"1"`: 미리 보기 또는 예고편
* `"2"`: 클립
* `"3"`: 기타

참여를 측정할 때 트레일러 및 클립과 같은 짧은 형식의 콘텐츠에서 전체 프로그램 보기를 분리하는 데 사용합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.type` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.sessionDetails.showType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.type` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.sessionDetails` 내에서 `showType`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        showType: "0"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

표시 형식을 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.SHOW_TYPE` 사용.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW_TYPE] = "0"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

표시 형식을 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.SHOW_TYPE` 사용.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW_TYPE] = "0"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `showType`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "showType": "0"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.sessionDetails` 내의 `showType`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "showType": "0"
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

`ADB.Media.VideoMetadataKeys.ShowType`을(를) 사용하여 `contextData` 개체에 표시 형식을 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.ShowType] = "0";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`trackSessionStart`을(를) 호출하기 전에 `ADBMobile.media.VideoMetadataKeys.SHOW_TYPE`을(를) 사용하여 미디어 개체의 `StandardMediaMetadata` 속성에 표시 형식을 설정하십시오.

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.SHOW_TYPE] = "0";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB 미디어 컬렉션 API]

`params` 개체에 `media.showType` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.showType": "0"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.

>[!ENDTABS]
