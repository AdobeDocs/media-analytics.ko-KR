---
title: 광고 길이
description: 각 광고의 길이를 초 단위로 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 14%

---


# 광고 길이

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**광고 길이**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [광고 길이](/help/reporting/dimensions/ad-length.md)를 참조하세요.*

>[!ENDSHADEBOX]

광고 길이 변수는 광고 기간(초)입니다. 모든 `media.adStart` 이벤트에 설정합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.ad.length` |
| **XDM 컬렉션 필드** | [`mediaCollection.advertisingDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.ad.length` |
| **필수** | 예 |
| **전송 시점** | [광고 시작](/help/implementation/events/ads/ad-start.md), 광고 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.advertisingDetails` 내에서 `length`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        length: 15
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

광고 길이를 `createAdObject`에 네 번째 인수로 전달합니다(초).

**iOS(Swift)**

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

**Android(Kotlin)**

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0L,
                                    15.0)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

## Roku(BrightScript)

`media.adStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `mediaCollection.advertisingDetails` 내에서 `length`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "length": 15,
                "podPosition": 0,
                "playerName": "Roku Player"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.advertisingDetails` 내에서 `length`을(를) 사용하여 [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) 끝점을 호출합니다.

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

광고 길이를 `ADB.Media.createAdObject`에 네 번째 인수로 전달합니다(초).

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",
  "ad-2125",
  0,
  15
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## Media Collection API

`adStart` POST 요청의 `params` 개체에 `media.ad.length` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.length": 15
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
