---
title: 광고 URL
description: 각 광고에 대한 광고 크리에이티브의 URL을 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 10%

---


# 광고 URL

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**Creative URL**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [Creative URL](/help/reporting/dimensions/creative-url.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

광고 크리에이티브 URL 변수는 광고 크리에이티브의 URL입니다. URL 자체가 분석에 중요한 경우(예: CDN 경로 또는 광고 버전 구분) 변수를 사용하여 각 광고 문안의 자산 위치를 추적합니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.ad.creativeURL` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.ad.creativeURL` |
| **필수** | 아니요 |
| **전송 시점** | [광고 시작](/help/implementation/events/ads/ad-start.md), 광고 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.advertisingDetails` 내에서 `creativeURL`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        creativeURL: "https://cdn.example.com/ads/creative-987.mp4"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Creative URL을 HashMap 인수의 메타데이터 키로 `trackEvent(AdStart)`에 전달합니다. `MediaConstants.AdMetadataKeys.CREATIVE_URL` 사용.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Creative URL을 HashMap 인수의 메타데이터 키로 `trackEvent(AdStart)`에 전달합니다. `MediaConstants.AdMetadataKeys.CREATIVE_URL` 사용.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku]

`media.adStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `xdm.mediaCollection.advertisingDetails` 내에서 `creativeURL`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.advertisingDetails` 내에서 `creativeURL`을(를) 사용하여 [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) 끝점을 호출합니다.

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
          "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`ADB.Media.AdMetadataKeys.CreativeUrl`을(를) 사용하여 `contextData` 개체에 크리에이티브 URL을 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeUrl] = "https://cdn.example.com/ads/creative-987.mp4";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

표준 광고 메타데이터 개체에서 `ADBMobile.media.AdMetadataKeys.CREATIVE_URL`을(를) 사용하여 크리에이티브 URL을 설정합니다.

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB 미디어 컬렉션 API]

`params` 개체에 `media.ad.creativeURL` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.

>[!ENDTABS]
