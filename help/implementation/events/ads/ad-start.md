---
title: 광고 시작
description: 개별 광고가 재생되기 시작했음을 신호.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 14%

---


# 광고 시작

광고 시작 이벤트는 개별 광고가 재생을 시작했음을 나타냅니다. [광고 브레이크 시작](ad-break-start.md)/[광고 브레이크 완료](ad-break-complete.md) 쌍 내에서 발생해야 합니다.

* **필수 구성 요소**: [세션 시작](../session/session-start.md), [광고 브레이크 시작](ad-break-start.md)
* **관련 지표**: [광고 시작](/help/reporting/metrics/ad-starts.md)

>[!IMPORTANT]
>
>이 이벤트는 단일 광고가 재생되는 경우에도 `adBreakStart` 및 `adBreakComplete` 북엔드로 둘러싸야 합니다. 이러한 북엔드가 없으면 광고 이벤트가 무시되고 광고 기간이 기본 콘텐츠 기간으로 계산됩니다.

## Web SDK

`eventType: "media.adStart"` 및 필수 `advertisingDetails`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        friendlyName: "Ford F-150",
        length: 15,
        playerName: "Freewheel",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

광고 이름, ID, pod 위치 및 길이를 `createAdObject`에 전달한 다음 `trackEvent`을(를) 호출합니다.

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
                                    0,
                                    15)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

## Roku(BrightScript)

`eventType: "media.adStart"` 및 필수 `advertisingDetails`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "friendlyName": "Ford F-150",
                "length": 15,
                "playerName": "Roku Player",
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

필요한 `advertisingDetails`을(를) 사용하여 [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) 끝점을 호출합니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

광고 이름, ID, 위치 및 길이를 `ADB.Media.createAdObject`에 전달합니다.

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, null);
```

## Media Collection API

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `adStart` POST 보내기:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "ad-2125",
    "media.ad.name": "Ford F-150",
    "media.ad.length": 15,
    "media.ad.podPosition": 0
  }
}
```
