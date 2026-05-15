---
title: 광고 브레이크 시작
description: 광고 브레이크(하나 이상의 광고 시퀀스)의 시작 신호를 보냅니다.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 13%

---


# 광고 브레이크 시작

광고 브레이크 시작 이벤트는 광고 브레이크를 시작한다는 신호를 보냅니다. 광고 브레이크는 하나 이상의 광고 시퀀스입니다. `adStart`, `adComplete` 및 `adSkip` 이벤트마다 `adBreakStart`과(와) `adBreakComplete` 쌍 사이에 발생해야 하며, 단일 광고가 재생되는 경우에도 마찬가지입니다.

* **필수 구성 요소**: [세션 시작](../session/session-start.md)
* **관련 지표**: 없음

>[!IMPORTANT]
>
>광고 이벤트(`adStart`, `adComplete`, `adSkip`)는 `adBreakStart` 및 `adBreakComplete` 북엔드 없이 무시됩니다. 광고 지속 시간이 없으면 광고 지속 시간은 집계된 보고 데이터에 영향을 주는 기본 콘텐츠 지속 시간으로 인한 것입니다.

## Web SDK

`eventType: "media.adBreakStart"` 및 필수 `advertisingPodDetails`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

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

광고 브레이크 이름, 위치 및 시작 시간을 `createAdBreakObject`에 전달한 다음 `trackEvent`을(를) 호출합니다.

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
                                              1,
                                              0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku(BrightScript)

`eventType: "media.adBreakStart"` 및 필수 `advertisingPodDetails`(으)로 `sendMediaEvent` 호출:

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

필요한 `advertisingPodDetails`(으)로 [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) 끝점을 호출합니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingPodDetails": {
          "index": 0,
          "offset": 0
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

광고 브레이크 이름, 위치 및 시작 시간을 `ADB.Media.createAdBreakObject`에 전달:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## Media Collection API

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `adBreakStart` POST 보내기:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll",
    "media.ad.podIndex": 1,
    "media.ad.podSecond": 0
  }
}
```
