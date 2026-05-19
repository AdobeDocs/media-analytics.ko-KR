---
title: 광고 건너뛰기
description: 뷰어가 광고를 건너뛰었다는 신호를 보냅니다.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 15%

---


# 광고 건너뛰기

광고 건너뛰기 이벤트는 뷰어가 완료되기 전에 광고를 건너뛰었다는 신호를 보냅니다. 뷰어가 건너뛰기 단추를 선택하면 보냅니다. 광고가 완료될 때까지 재생되는 경우 대신 [광고 완료](ad-complete.md)를 보냅니다.

* **필수 구성 요소**: [세션 시작](../session/session-start.md), [광고 브레이크 시작](ad-break-start.md), [광고 시작](ad-start.md)
* **관련 지표**: 없음

>[!IMPORTANT]
>
>이 이벤트는 단일 광고가 재생되는 경우에도 `adBreakStart` 및 `adBreakComplete` 북엔드로 둘러싸야 합니다. 이러한 북엔드가 없으면 광고 이벤트가 무시되고 광고 기간이 기본 콘텐츠 기간으로 계산됩니다.

## Web SDK

`eventType: "media.adSkip"`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 5
    }
  }
});
```

## Mobile SDK

`AdSkip` 이벤트 형식으로 `trackEvent`을(를) 호출합니다.

**iOS(Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

**Android(Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

## Roku(BrightScript)

`eventType: "media.adSkip"`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adSkip",
        "mediaCollection": {
            "playhead": 5
        }
    }
})
```

## Media Edge API

[adSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adskip) 끝점을 호출합니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 5
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

`AdSkip` 이벤트 형식으로 `trackEvent` 호출:

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

## Media Collection API

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `adSkip` POST 보내기:

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```
