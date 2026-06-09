---
title: 광고주
description: 각 광고에 출연한 회사 또는 브랜드를 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 10%

---


# 광고주

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**Advertiser**&#x200B;변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대해서는 [Advertiser](/help/reporting/dimensions/advertiser.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

광고주 변수는 광고에 포함된 회사 또는 브랜드입니다(예: `"Ford"` 또는 `"Coca-Cola"`). 광고주별로 참여 및 완료를 분류하려면 변수를 사용하십시오.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.ad.advertiser` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.advertisingDetails.advertiser`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.ad.advertiser` |
| **필수** | 아니요 |
| **전송 시점** | [광고 시작](/help/implementation/events/ads/ad-start.md), 광고 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.advertisingDetails` 내에서 `advertiser`을(를) 설정합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        advertiser: "Ford"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

광고주를 HashMap 인수의 메타데이터 키로 `trackEvent(AdStart)`에 전달합니다. `MediaConstants.AdMetadataKeys.ADVERTISER` 사용.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

광고주를 HashMap 인수의 메타데이터 키로 `trackEvent(AdStart)`에 전달합니다. `MediaConstants.AdMetadataKeys.ADVERTISER` 사용.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

`media.adStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `xdm.mediaCollection.advertisingDetails` 내에서 `advertiser`을(를) 설정합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "advertiser": "Ford"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.advertisingDetails` 내에서 `advertiser`을(를) 사용하여 [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) 끝점을 호출합니다.

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
          "advertiser": "Ford"
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

`ADB.Media.AdMetadataKeys.Advertiser`을(를) 사용하여 `contextData` 개체에 광고주를 전달합니다.

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.Advertiser] = "Ford";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

표준 광고 메타데이터 개체에서 `ADBMobile.media.AdMetadataKeys.ADVERTISER`을(를) 사용하여 광고주를 설정합니다.

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.ADVERTISER] = "Sample advertiser";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

표준 광고 메타데이터 개체에서 `MEDIA_AdMetadataKeyADVERTISER`을(를) 사용하여 광고주를 설정합니다.

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeyADVERTISER] = "Sample advertiser"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB 미디어 컬렉션 API]

`params` 개체에 `media.ad.advertiser` 포함:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.advertiser": "Ford"
  }
}
```

전체 요청 구조에 대해서는 [Media Collection API 이벤트 참조](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)를 참조하십시오.

>[!ENDTABS]
