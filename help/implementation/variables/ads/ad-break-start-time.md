---
title: 광고 브레이크 시작 시간
description: 콘텐츠 내부의 광고 브레이크 시작 시간(오프셋)을 초 단위로 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 12%

---


# 광고 브레이크 시작 시간

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**광고 브레이크 시작 시간**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [Pod 위치](/help/reporting/dimensions/pod-position.md)을 참조하세요.*

>[!ENDSHADEBOX]

광고 브레이크 시작 시간 변수는 콘텐츠 내의 광고 브레이크 오프셋(초)입니다. 프리롤의 경우 값은 `0`이고, 미드롤의 경우 값은 브레이크가 시작되는 플레이헤드 위치입니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.ad.podSecond` |
| **XDM 컬렉션 필드** | [`mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.ad.podSecond` |
| **필수** | 예 |
| **전송 시점** | [광고 브레이크 시작](/help/implementation/events/ads/ad-break-start.md), 광고 닫기 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.advertisingPodDetails` 내에서 `offset`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "mid-roll-1",
        index: 2,
        offset: 90
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

`createAdBreakObject`에 세 번째 인수로 시작 시간을 초 단위로 전달합니다.

**iOS(Swift)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android(Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku(BrightScript)

`media.adBreakStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `mediaCollection.advertisingPodDetails` 내에서 `offset`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "mid-roll-1",
                "index": 2,
                "offset": 90
            },
            "playhead": 90
        }
    }
})
```

## Media Edge API

`mediaCollection.advertisingPodDetails` 내에서 `offset`을(를) 사용하여 [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "index": 2,
          "offset": 90
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Media SDK

시작 시간을 `ADB.Media.createAdBreakObject`에 세 번째 인수로 전달합니다.

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## Media Collection API

`adBreakStart` POST 요청의 `params` 개체에 `media.ad.podSecond` 포함:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podSecond": 90
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
