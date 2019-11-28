---
title: 세션 응답이 느린 경우 큐에 이벤트 저장
description: null
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 세션 응답이 느린 경우 큐에 이벤트 저장{#queueing-events-when-sessions-response-is-slow}

Media Collection API는 RESTful입니다. 즉, HTTP 요청을 작성하고 응답을 기다립니다. 이는 비디오 재생 시작 시 세션 ID를 가져오도록 [세션 요청](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)을 작성할 때에만 중요한 시점입니다. 이는 모든 후속 추적 호출에 세션 ID가 필요하기 때문에 중요합니다.

(세션 ID 매개 변수와 함께) _세션이 백 엔드의 반환에 응답하기 전에_ 플레이어가 이벤트를 실행할 수 있습니다. 이 경우 앱은 [세션 요청](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)과 해당 응답 사이에 도착하는 모든 추적 이벤트를 큐에 추가해야 합니다. 세션 응답이 도착하면 먼저 큐에 있는 [이벤트](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)를 처리해야 [이벤트](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) 호출 시 _실시간_ 이벤트 처리를 시작할 수 있습니다.

>[!NOTE]
>
>[이벤트 요청](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)은 HTTP 응답 코드 외에 데이터를 고객에 다시 반환하지 않습니다.

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

**큐에 있는 이벤트 처리 -** 참조 플레이어가 다음과 같이 큐에 있는 이벤트를 처리합니다.

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

추적 이벤트가 발송할 때 추적 이벤트를 계속 처리합니다.
