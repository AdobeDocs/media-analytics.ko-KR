---
title: 광고 브레이크 시작 시간
description: 콘텐츠 내부의 광고 브레이크 시작 시간(오프셋)을 초 단위로 설정합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 6%

---


# 광고 브레이크 시작 시간

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**광고 브레이크 시작 시간**변수에 대한 데이터 수집을 다룹니다. 해당 보고 차원에 대한 [Pod 위치](/help/reporting/dimensions/pod-position.md)을 참조하세요.*

>[!ENDSHADEBOX]

광고 브레이크 시작 시간 변수는 콘텐츠 내의 광고 브레이크 오프셋(초)입니다. 프리롤의 경우 값은 `0`이고, 미드롤의 경우 값은 브레이크가 시작되는 플레이헤드 위치입니다.

| 속성 | 값 |
| --- | --- |
| **컨텍스트 데이터 변수** | `a.media.ad.podSecond` |
| **XDM 컬렉션 필드** | [`xdm.mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Audience Manager 트레이트** | `c_contextdata.a.media.ad.podSecond` |
| **필수** | 예 |
| **전송 시점** | [광고 브레이크 시작](/help/implementation/events/ads/ad-break-start.md), 광고 닫기 |

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

[`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview)을(를) 호출할 때 `xdm.mediaCollection.advertisingPodDetails` 내에서 `offset`을(를) 설정합니다.

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

>[!TAB iOS]

`createAdBreakObject`에 세 번째 인수로 시작 시간을 초 단위로 전달합니다.

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

`createAdBreakObject`에 세 번째 인수로 시작 시간을 초 단위로 전달합니다.

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku Edge]

`media.adBreakStart`에 대해 `sendMediaEvent`을(를) 호출할 때 `xdm.mediaCollection.advertisingPodDetails` 내에서 `offset`을(를) 설정합니다.

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

>[!TAB 미디어 Edge API]

`xdm.mediaCollection.advertisingPodDetails` 내에서 `offset`을(를) 사용하여 [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) 끝점을 호출합니다.

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

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

시작 시간을 `ADB.Media.createAdBreakObject`에 세 번째 인수로 전달합니다.

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

`ADBMobile.media.createAdBreakObject`에 세 번째 인수로 시작 시간을 초 단위로 전달합니다.

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Roku 2.x]

`adb_media_init_adbreakinfo`에 두 번째 인수로 시작 시간을 초 단위로 전달합니다. Roku 매개 변수 순서: `name, startTime, position`을(를) 참고하십시오.

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("mid-roll-1", 90.0, 2)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
```

>[!TAB 미디어 컬렉션 API]

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

>[!ENDTABS]
