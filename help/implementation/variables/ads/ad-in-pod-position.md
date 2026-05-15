---
title: Pod 위치의 광고
description: 상위 광고 브레이크 내에 광고의 색인 위치를 설정합니다. 첫 번째 광고에는 색인 0이 있습니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 12%

---


# Pod 위치의 광고

>[!BEGINSHADEBOX]

*이 페이지에서는 pod 위치의&#x200B;**Ad**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대해서는 [Pod 위치의 광고](/help/reporting/dimensions/ad-in-pod-position.md)를 참조하십시오.*

>[!ENDSHADEBOX]

pod의 광고 위치 변수는 상위 광고 브레이크 내에 있는 광고의 인덱싱된 위치입니다. Pod의 첫 번째 광고에 `0` 색인이 있고, 두 번째 광고에 `1` 색인이 있는 식입니다. 차원을 사용하여 광고 브레이크 내에서 위치별로 참여 및 완료를 비교합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.ad.podPosition` |
| **XDM 컬렉션 필드** | [`mediaCollection.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.ad.podPosition` |
| **필수** | 예 |
| **전송 시점** | [광고 시작](/help/implementation/events/ads/ad-start.md), 광고 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.advertisingDetails` 내에서 `podPosition`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

위치를 `createAdObject`에 세 번째 인수로 전달합니다.

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

`media.adStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `mediaCollection.advertisingDetails` 내에서 `podPosition`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "podPosition": 0,
                "length": 15,
                "playerName": "Roku Player"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.advertisingDetails` 내에서 `podPosition`을(를) 사용하여 [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) 끝점을 호출합니다.

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

위치를 `ADB.Media.createAdObject`에 세 번째 인수로 전달합니다.

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

`params` 개체에 `media.ad.podPosition` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.podPosition": 0
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
