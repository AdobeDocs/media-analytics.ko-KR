---
title: 광고 완료
description: 개별 광고의 재생이 완료되었음을 나타냅니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 8%

---


# 광고 완료

광고 완료 이벤트는 개별 광고가 재생을 완료했다는 신호를 보냅니다. 광고가 재생된 후 완료 시까지 보냅니다. 뷰어가 광고를 건너뛸 경우 대신 [광고 건너뛰기](ad-skip.md)를 보내십시오.

* **필수 구성 요소**: [세션 시작](../session/session-start.md), [광고 브레이크 시작](ad-break-start.md), [광고 시작](ad-start.md)
* **관련 지표**: [[!UICONTROL 광고 완료]](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>이 이벤트는 단일 광고가 재생되는 경우에도 `adBreakStart` 및 `adBreakComplete` 북엔드로 둘러싸야 합니다. 이러한 북엔드가 없으면 광고 이벤트가 무시되고 광고 기간이 기본 콘텐츠 기간으로 계산됩니다.

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

`eventType: "media.adComplete"`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 15
    }
  }
});
```

>[!TAB iOS]

`AdComplete` 이벤트 형식으로 `trackEvent`을(를) 호출합니다.

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

>[!TAB Android]

`AdComplete` 이벤트 형식으로 `trackEvent`을(를) 호출합니다.

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

>[!TAB Roku Edge]

`eventType: "media.adComplete"`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adComplete",
        "mediaCollection": {
            "playhead": 15
        }
    }
})
```

>[!TAB 미디어 Edge API]

[adComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adcomplete) 끝점 호출:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 15
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

`AdComplete` 이벤트 형식으로 `trackEvent` 호출:

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

>[!TAB Chromecast]

`AdComplete` 이벤트 형식으로 `trackEvent` 호출:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
```

>[!TAB Roku 2.x]

`MEDIA_AD_COMPLETE` 이벤트 형식으로 `mediaTrackEvent` 호출:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_COMPLETE)
```

>[!TAB 미디어 컬렉션 API]

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `adComplete` POST 보내기:

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```

>[!ENDTABS]
