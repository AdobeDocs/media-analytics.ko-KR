---
title: 일시 중지 시작
description: 사용자가 미디어 재생을 일시 중지했음을 나타냅니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%

---


# 일시 중지 시작

일시 중지 시작 이벤트는 사용자가 재생을 일시 중지했음을 알립니다. 별도의 다시 시작 이벤트가 없습니다. 재생이 다시 시작될 때 [재생](play.md) 이벤트를 보내십시오.

* **필수 구성 요소**: [세션 시작](../session/session-start.md)
* **관련 지표**: [[!UICONTROL 이벤트 일시 중지]](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>다시 시작 이벤트 유형이 없습니다. 다시 시작은 `pauseStart` 이후에 [`play`](play.md) 이벤트를 보낼 때 추론됩니다.

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

`eventType: "media.pauseStart"`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.pauseStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 30
    }
  }
});
```

>[!TAB iOS]

사용자가 재생을 일시 중지하면 `trackPause`을(를) 호출합니다.

```swift
tracker.trackPause()
```

>[!TAB Android]

사용자가 재생을 일시 중지하면 `trackPause`을(를) 호출합니다.

```kotlin
tracker.trackPause()
```

>[!TAB Roku Edge]

`eventType: "media.pauseStart"`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.pauseStart",
        "mediaCollection": {
            "playhead": 30
        }
    }
})
```

>[!TAB 미디어 Edge API]

[pauseStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/pausestart/) 끝점 호출:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/pauseStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.pauseStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 30
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

사용자가 재생을 일시 중지하면 `trackPause`을(를) 호출합니다.

```javascript
tracker.trackPause();
```

>[!TAB Chromecast]

사용자가 재생을 일시 중지하면 `trackPause`을(를) 호출합니다.

```javascript
ADBMobile.media.trackPause();
```

>[!TAB Roku 2.x]

사용자가 재생을 일시 중지하면 `mediaTrackPause`을(를) 호출합니다.

```brightscript
ADBMobile().mediaTrackPause()
```

>[!TAB 미디어 컬렉션 API]

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `pauseStart` POST 보내기:

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```

>[!ENDTABS]
