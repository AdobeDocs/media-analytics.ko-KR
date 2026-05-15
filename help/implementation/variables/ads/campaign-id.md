---
title: 캠페인 ID
description: 캠페인별로 참여를 집계할 수 있도록 각 광고에 대한 캠페인 식별자를 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 15%

---


# 캠페인 ID

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**캠페인 ID**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [Campaign ID](/help/reporting/dimensions/campaign-id.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

캠페인 ID 변수는 크리에이티브가 속한 광고 캠페인을 식별합니다. 모든 문자열 값(일반적으로 광고 서버 플랫폼의 캠페인 ID)은 사용할 수 있습니다. 캠페인을 공유하는 여러 크리에이티브 간에 참여를 롤업하려면 변수를 사용하십시오.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.ad.campaign` |
| **XDM 컬렉션 필드** | [`mediaCollection.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.ad.campaign` |
| **필수** | 아니요 |
| **전송 시점** | [광고 시작](/help/implementation/events/ads/ad-start.md), 광고 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.advertisingDetails` 내에서 `campaignID`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        campaignID: "fall-2024"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

캠페인 ID를 HashMap 인수의 메타데이터 키로 `trackEvent(AdStart)`에 전달합니다. `MediaConstants.AdMetadataKeys.CAMPAIGN_ID` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku(BrightScript)

`media.adStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `mediaCollection.advertisingDetails` 내에서 `campaignID`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "campaignID": "fall-2024"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.advertisingDetails` 내에서 `campaignID`을(를) 사용하여 [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) 끝점을 호출합니다.

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
          "podPosition": 0,
          "campaignID": "fall-2024"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.AdMetadataKeys.CampaignId`을(를) 사용하여 `contextData` 개체에 캠페인 ID를 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CampaignId] = "fall-2024";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Media Collection API

`params` 개체에 `media.ad.campaignId` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.campaignId": "fall-2024"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
