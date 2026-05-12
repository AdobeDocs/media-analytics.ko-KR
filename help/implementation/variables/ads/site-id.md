---
title: 사이트 ID
description: 광고 배치 사이트별로 구분을 활성화하려면 각 광고에 대한 광고 사이트 ID를 설정하십시오.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 17%

---


# 사이트 ID

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**사이트 ID**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [사이트 ID](/help/reporting/dimensions/site-id.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

사이트 ID 변수는 광고 사이트를 식별합니다. 모든 문자열 값(일반적으로 광고 서버 플랫폼의 ID)은 사용할 수 있습니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.ad.site` |
| **XDM 컬렉션 필드** | [`mediaCollection.advertisingDetails.siteID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **필수** | 아니요 |
| **전송 시점** | 광고 시작, 광고 종료 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.advertisingDetails` 내에서 `siteID`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        siteID: "site-42"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

사이트 ID를 HashMap 인수의 메타데이터 키로 `trackEvent(AdStart)`에 전달합니다. `MediaConstants.AdMetadataKeys.SITE_ID` 사용.

**iOS(Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.SITE_ID] = "site-42"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android(Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.SITE_ID] = "site-42"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku(BrightScript)

`media.adStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `mediaCollection.advertisingDetails` 내에서 `siteID`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "siteID": "site-42"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.advertisingDetails` 내에서 `siteID`을(를) 사용하여 [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) 끝점을 호출합니다.

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
          "siteID": "site-42"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

`ADB.Media.AdMetadataKeys.SiteId`을(를) 사용하여 `contextData` 개체에 사이트 ID를 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.SiteId] = "site-42";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Media Collection API

`params` 개체에 `media.ad.siteId` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.siteId": "site-42"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
