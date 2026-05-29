---
title: 재생
description: 미디어 플레이어가 재생 상태에 들어왔다는 신호를 보냅니다.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 10%

---


# 재생

재생 이벤트는 미디어 플레이어가 재생 상태를 재생으로 변경했다는 신호를 보냅니다. 콘텐츠의 초기 시작 시, 자동 재생 시 및 일시 정지 또는 버퍼 이후 플레이어가 다시 시작될 때마다 전송합니다. 별도의 다시 시작 이벤트가 없습니다. [일시 중지 시작](pause-start.md) 또는 [버퍼 시작](buffer-start.md) 이후의 재생 이벤트가 다시 시작 이벤트로 사용됩니다.

* **필수 구성 요소**: [세션 시작](../session/session-start.md)
* **관련 지표**: [[!UICONTROL 콘텐츠 시작]](/help/reporting/metrics/content-starts.md)

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

`eventType: "media.play"`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

미디어 플레이어가 재생을 시작하거나 다시 시작할 때 `trackPlay`을(를) 호출합니다.

```swift
tracker.trackPlay()
```

>[!TAB Android]

미디어 플레이어가 재생을 시작하거나 다시 시작할 때 `trackPlay`을(를) 호출합니다.

```kotlin
tracker.trackPlay()
```

>[!TAB Roku]

`eventType: "media.play"`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

>[!TAB 미디어 Edge API]

[play](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/) 끝점 호출:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
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

미디어 플레이어가 재생을 시작하거나 다시 시작할 때 `trackPlay`을(를) 호출합니다.

```javascript
tracker.trackPlay();
```

>[!TAB Chromecast]

미디어 플레이어가 재생을 시작하거나 다시 시작할 때 `trackPlay`을(를) 호출합니다.

```javascript
ADBMobile.media.trackPlay();
```

>[!TAB 미디어 컬렉션 API]

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `play` POST 보내기:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```

>[!ENDTABS]
