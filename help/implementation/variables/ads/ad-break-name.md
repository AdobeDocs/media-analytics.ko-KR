---
title: 광고 브레이크 이름
description: 상위 광고 브레이크의 친숙한 이름을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 12%

---


# 광고 브레이크 이름

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**광고 브레이크 이름**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [Pod 이름](/help/reporting/dimensions/pod-name.md)을 참조하세요.*

>[!ENDSHADEBOX]

광고 브레이크 이름 변수는 친숙한 광고 브레이크 이름입니다(예: `"pre-roll"`, `"mid-roll-1"`, `"post-roll"`). 이 값은 개별 광고가 아닌 광고 브레이크 개체에 설정됩니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.ad.podFriendlyName` |
| **XDM 컬렉션 필드** | [`mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **필수** | 예(모바일 SDK), 아니요(Edge, Media Collection API) |
| **전송 시점** | 광고 시작, 광고 종료 |

## Web SDK

`media.adBreakStart`에 대해 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `mediaCollection.advertisingPodDetails` 내에서 `friendlyName`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "pre-roll",
        index: 1,
        offset: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

광고 브레이크 이름을 첫 번째(`name`) 인수로 `createAdBreakObject`에 전달한 다음 광고 시작 이벤트 전에 광고 브레이크 시작 이벤트를 추적합니다.

**iOS(Swift)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android(Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku(BrightScript)

`media.adBreakStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `mediaCollection.advertisingPodDetails` 내에서 `friendlyName`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "pre-roll",
                "index": 1,
                "offset": 0
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.advertisingPodDetails` 내에서 `friendlyName`을(를) 사용하여 [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) 끝점을 호출합니다.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "friendlyName": "pre-roll",
          "index": 1,
          "offset": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

광고 브레이크 이름을 첫 번째 인수로 `ADB.Media.createAdBreakObject`에 전달합니다.

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## Media Collection API

`adBreakStart` POST 요청의 `params` 개체에 `media.ad.podFriendlyName` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.
