---
title: Ping
description: 하트비트를 전송하여 미디어 세션을 유지하고 일정한 간격으로 재생 진행률을 추적합니다.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 1%

---


# Ping

ping 이벤트는 세션을 활성 상태로 유지하고 재생 진행률을 추적하는 하트비트입니다. 재생 도중 타이머로 보냅니다. Mobile SDK에서는 Ping이 자동으로 전송됩니다. 다른 모든 플랫폼에서는 지정된 간격에 따라 수동으로 전송해야 합니다.

* **기본 컨텐츠**: 재생이 시작된 후 먼저 10초 후에 ping하고, 그 후에는 10초마다 ping합니다.
* **광고 콘텐츠**: 광고 추적 중 1초마다

Ping 요청 본문에 `params` 개체를 포함하지 마십시오.

* **필수 구성 요소**: [세션 시작](../session/session-start.md)
* **관련 지표**: 없음

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

`eventType: "media.ping"`(으)로 반복 `sendEvent` 통화를 예약합니다. 각 호출에서 `playhead`을(를) 현재 재생 위치로 업데이트합니다.

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.ping",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 10
    }
  }
});
```

>[!TAB iOS]

Mobile SDK은 ping 이벤트를 자동으로 전송합니다. 명시적인 호출이 필요하지 않습니다.

>[!TAB Android]

Mobile SDK은 ping 이벤트를 자동으로 전송합니다. 명시적인 호출이 필요하지 않습니다.

>[!TAB Roku Edge]

`eventType: "media.ping"`(으)로 반복 `sendMediaEvent` 통화를 예약합니다. 각 호출에서 `playhead`을(를) 현재 재생 위치로 업데이트합니다.

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.ping",
        "mediaCollection": {
            "playhead": 10
        }
    }
})
```

>[!TAB 미디어 Edge API]

타이머에서 [ping](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ping/) 끝점을 호출합니다. Adobe에서는 기본 재생이 시작된 후 첫 번째 ping은 10초 후를, 10초 후를, 광고 추적 중에는 1초를 권장합니다.

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/ping?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.ping",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 10
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

Media SDK은 ping 이벤트를 자동으로 전송합니다. 명시적인 호출이 필요하지 않습니다.

>[!TAB Chromecast]

Chromecast SDK은 ping 이벤트를 자동으로 전송합니다. 명시적인 호출이 필요하지 않습니다.

>[!TAB Roku 2.x]

이벤트 루프에서 `processMediaMessages`을(를) 호출하는 한 Media SDK에서 ping 이벤트를 자동으로 보냅니다. 각 ping이 현재 위치를 보고하도록 플레이헤드를 업데이트합니다.

```brightscript
ADBMobile().mediaUpdatePlayhead(10)
```

>[!TAB 미디어 컬렉션 API]

타이머의 [이벤트 끝점](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)에 `ping` POST를 보냅니다. `params` 개체 포함 안 함:

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```

>[!ENDTABS]
