---
title: 세션 완료
description: 뷰어가 기본 콘텐츠의 끝에 도달했음을 신호로 보냅니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 8%

---


# 세션 완료

세션 완료 이벤트는 뷰어가 기본 콘텐츠의 끝에 도달했음을 알립니다. 세션을 즉시 닫지는 않습니다. 세션이 자연히 만료될 때까지 열려 있습니다. 세션을 즉시 닫으려면 대신 [세션 종료](session-end.md)를 호출하십시오.

* **필수 구성 요소**: [세션 시작](session-start.md)
* **관련 지표**: [[!UICONTROL 콘텐츠 완료]](/help/reporting/metrics/content-completes.md)

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

`eventType: "media.sessionComplete"`(으)로 [`sendEvent`](https://experienceleague.adobe.com/kr/docs/experience-platform/collection/js/commands/sendevent/overview) 호출:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 128
    }
  }
});
```

>[!TAB iOS]

미디어 플레이어가 콘텐츠의 끝에 도달하면 `trackComplete`을(를) 호출합니다.

```swift
tracker.trackComplete()
```

>[!TAB Android]

미디어 플레이어가 콘텐츠의 끝에 도달하면 `trackComplete`을(를) 호출합니다.

```kotlin
tracker.trackComplete()
```

>[!TAB Roku Edge]

`eventType: "media.sessionComplete"`(으)로 `sendMediaEvent` 호출:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
            "playhead": 128
        }
    }
})
```

>[!TAB 미디어 Edge API]

[sessionComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessioncomplete) 끝점 호출:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 128
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

미디어 플레이어가 콘텐츠의 끝에 도달하면 `trackComplete`을(를) 호출합니다.

```javascript
tracker.trackComplete();
```

>[!TAB Chromecast]

미디어 플레이어가 콘텐츠의 끝에 도달하면 `trackComplete`을(를) 호출합니다.

```javascript
ADBMobile.media.trackComplete();
```

>[!TAB Roku 2.x]

미디어 플레이어가 콘텐츠의 끝에 도달하면 `mediaTrackComplete`을(를) 호출합니다.

```brightscript
ADBMobile().mediaTrackComplete()
```

>[!TAB 미디어 컬렉션 API]

[이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `sessionComplete` POST 보내기:

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```

>[!ENDTABS]
