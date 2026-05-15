---
title: 광고 플레이어 이름
description: 광고를 렌더링하는 플레이어의 이름을 설정합니다. 광고 플레이어는 기본 콘텐츠 플레이어와 다를 수 있습니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 11%

---


# 광고 플레이어 이름

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**광고 플레이어 이름**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [광고 플레이어 이름](/help/reporting/dimensions/ad-player-name.md)을 참조하세요.*

>[!ENDSHADEBOX]

광고 플레이어 이름 변수는 각 광고를 렌더링한 플레이어를 식별합니다(예: `"Freewheel"`, `"Google IMA"`). 광고가 서버측 광고 삽입 서비스에 의해 에서 결합되는 경우 광고 플레이어는 기본 컨텐츠 플레이어와 다를 수 있습니다. 이 변수를 사용하여 광고 서비스 스택 간 품질과 완료를 비교할 수 있습니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.ad.playerName` |
| **XDM 컬렉션 필드** | [`mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.ad.playerName` |
| **필수** | 예 |
| **전송 시점** | [광고 시작](/help/implementation/events/ads/ad-start.md), 광고 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.advertisingDetails` 내에서 `playerName`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        playerName: "Freewheel"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

광고 플레이어 이름을 메타데이터 HashMap 인수의 `MediaConstants.AdMetadataKeys.AD_PLAYER` 키로 `trackEvent(AdStart)`에 전달합니다.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku(BrightScript)

`media.adStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `mediaCollection.advertisingDetails` 내에서 `playerName`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "playerName": "Freewheel",
                "length": 15,
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.advertisingDetails` 내에서 `playerName`을(를) 사용하여 [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.AdMetadataKeys.AdPlayer`을(를) 사용하여 `contextData` 개체에 광고 플레이어 이름을 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Media Collection API

`adStart` POST 요청의 `params` 개체에 `media.ad.playerName` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.playerName": "Freewheel"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
