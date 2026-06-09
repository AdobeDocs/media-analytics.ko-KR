---
title: 광고 브레이크 완료
description: 광고 브레이크의 모든 광고가 완료되었음을 알립니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 9%

---


# 광고 브레이크 완료

광고 브레이크 완료 이벤트는 광고 브레이크의 모든 광고가 완료되었음을(완료됨 또는 건너뜀) 신호를 보냅니다. [광고 브레이크 시작](ad-break-start.md)에 의해 열린 광고 브레이크를 닫습니다.

* **필수 구성 요소**: [세션 시작](../session/session-start.md), [광고 브레이크 시작](ad-break-start.md)
* **관련 지표**: 없음

>[!IMPORTANT]
>
>모든 `adBreakStart`에 일치하는 `adBreakComplete`이(가) 있어야 합니다. 닫는 북엔드가 없으면 광고 이벤트는 무시되고 광고 기간은 기본 콘텐츠에 귀속됩니다.

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

`eventType: "media.adBreakComplete"`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

`AdBreakComplete` 이벤트 형식으로 `trackEvent`을(를) 호출합니다.

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

>[!TAB Android]

`AdBreakComplete` 이벤트 형식으로 `trackEvent`을(를) 호출합니다.

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

>[!TAB Roku Edge]

`eventType: "media.adBreakComplete"`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakComplete",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

[adBreakComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakcomplete) 끝점을 호출합니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`AdBreakComplete` 이벤트 형식으로 `trackEvent` 호출:

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

>[!TAB Chromecast]

`AdBreakComplete` 이벤트 형식으로 `trackEvent` 호출:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete);
```

>[!TAB Roku 2.x]

`MEDIA_AD_BREAK_COMPLETE` 이벤트 형식으로 `mediaTrackEvent` 호출:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_COMPLETE)
```

>[!TAB 미디어 컬렉션 API]

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `adBreakComplete` POST 보내기:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```

>[!ENDTABS]
