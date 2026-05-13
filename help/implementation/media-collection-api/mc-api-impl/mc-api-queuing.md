---
title: 세션 응답이 느린 경우 큐에 이벤트 저장
description: 플레이어에서 이벤트를 실행한 후 세션 ID가 반환될 때 수행할 작업에 대해 알아봅니다.
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/maOCcXZJkPef7edi3UtaSIJKa-4x9byaH6Qzt2eDR2Y
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 205
ht-degree: 90%

---

# 세션 응답이 느린 경우 큐에 이벤트 저장{#queueing-events-when-sessions-response-is-slow}

Media Collection API는 RESTful입니다. 즉, HTTP 요청을 작성하고 응답을 기다립니다. 이는 비디오 재생 시작 시 세션 ID를 가져오도록 [세션 요청](../mc-api-ref/mc-api-sessions-req.md)을 작성할 때에만 중요한 시점입니다. 이는 모든 후속 추적 호출에 세션 ID가 필요하기 때문에 중요합니다.

(세션 ID 매개 변수와 함께) _세션이 백 엔드의 반환에 응답하기 전에_ 플레이어가 이벤트를 실행할 수 있습니다. 이 경우 앱은 [세션 요청](../mc-api-ref/mc-api-sessions-req.md)과 해당 응답 사이에 도착하는 모든 추적 이벤트를 큐에 추가해야 합니다. 세션 응답이 도착하면 먼저 큐에 있는 [이벤트](../mc-api-ref/mc-api-events-req.md)를 처리해야 [이벤트](../mc-api-ref/mc-api-events-req.md) 호출 시 _실시간_ 이벤트 처리를 시작할 수 있습니다.

>[!NOTE]
>
>[이벤트 요청](../mc-api-ref/mc-api-events-req.md)은 HTTP 응답 코드 외에 데이터를 고객에 다시 반환하지 않습니다.

참조 플레이어에서 세션 ID를 수신하기 전에 이벤트를 처리하는 한 가지 방법을 확인합니다. 예:

```js
var eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```

**큐에 있는 이벤트 처리 -** 참조 플레이어는 큐에 있는 이벤트를 다음과 같이 처리합니다.

```js
    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```

발생하는 추적 이벤트를 계속 처리합니다.
