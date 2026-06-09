---
title: 자산 ID
description: EIDR 또는 TMS/Gracenote ID와 같은 미디어 에셋에 대한 안정적인 업계 식별자인 에셋 ID를 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 8%

---


# 자산 ID

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**자산 ID**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [자산 ID](/help/reporting/dimensions/asset-id.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

에셋 ID 변수는 기본 미디어 에셋에 대한 고유 식별자입니다(예: 에피소드 ID, 동영상 ID 또는 라이브 이벤트 ID). 일반적으로 EIDR, TMS/Gracenote 또는 Rovi와 같은 메타데이터 기관에서 출처하지만 독점 또는 사내 ID도 허용됩니다. 동일한 기본 에셋에 다른 콘텐츠 ID를 할당할 수 있는 배포 플랫폼 간 참여를 비교해야 할 때 사용합니다.

>[!NOTE]
>
>XDM 컬렉션 필드는 대문자 `ID`을(를) 사용합니다. `assetID`.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.asset` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.sessionDetails.assetID`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.asset` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.sessionDetails` 내에서 `assetID`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        assetID: "89745363"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

자산 ID를 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.ASSET_ID` 사용.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

자산 ID를 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.ASSET_ID` 사용.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

`createMediaSession`을(를) 사용하여 `sessionDetails` 내에서 `assetID`을(를) 설정합니다.

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "assetID": "89745363"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.sessionDetails` 내의 `assetID`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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
          "assetID": "89745363"
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

`ADB.Media.VideoMetadataKeys.AssetId`을(를) 사용하여 `contextData` 개체에 자산 ID를 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AssetId] = "89745363";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`trackSessionStart`을(를) 호출하기 전에 `ADBMobile.media.VideoMetadataKeys.ASSET_ID`을(를) 사용하여 미디어 개체의 `StandardMediaMetadata` 속성에 자산 ID를 설정합니다.

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.ASSET_ID] = "89745363";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

`mediaTrackSessionStart`을(를) 호출하기 전에 `MEDIA_VideoMetadataKeyASSET_ID`을(를) 사용하여 미디어 개체의 표준 메타데이터에서 자산 ID를 설정하십시오.

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyASSET_ID] = "89745363"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 미디어 컬렉션 API]

`params` 개체에 `media.assetId` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.assetId": "89745363"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 세션 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)를 참조하십시오.

>[!ENDTABS]
