---
title: 자산 ID
description: EIDR 또는 TMS/Gracenote ID와 같은 미디어 에셋에 대한 안정적인 업계 식별자인 에셋 ID를 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 12%

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
| **XDM 컬렉션 필드** | [`mediaCollection.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.asset` |
| **필수** | 아니요 |
| **전송 시점** | [세션 시작](/help/implementation/events/session/session-start.md), 세션 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.sessionDetails` 내에서 `assetID`을(를) 설정합니다.

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

## Mobile SDK

자산 ID를 HashMap 인수의 메타데이터 키로 `trackSessionStart`에 전달합니다. `MediaConstants.VideoMetadataKeys.ASSET_ID` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku(BrightScript)

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

## Media Edge API

`mediaCollection.sessionDetails` 내의 `assetID`을(를) 사용하여 [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) 끝점을 호출합니다.

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

## Media SDK

`ADB.Media.VideoMetadataKeys.AssetId`을(를) 사용하여 `contextData` 개체에 자산 ID를 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AssetId] = "89745363";

tracker.trackSessionStart(mediaInfo, contextData);
```

## Media Collection API

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
