---
seo-title: 세션 응답이 느린 경우 큐에 이벤트 저장
title: 세션 응답이 느린 경우 큐에 이벤트 저장
uuid: 39 ea 59 d 9-89 d 3-4087-a 806-48 a 43 ecf 0 c 98
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 세션 응답이 느린 경우 큐에 이벤트 저장{#queueing-events-when-sessions-response-is-slow}

Media Collection API는 RESTful입니다. 즉, HTTP 요청을 작성하고 응답을 기다립니다. This is an important point only for when you make a [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) to obtain a Session ID at the beginning of video playback. 이는 이후의 모든 추적 호출에 대해 세션 ID가 필요하기 때문에 중요합니다.

It is possible that your player may fire events _before the Sessions response returns_ (with the Session ID parameter) from the backend. If this occurs, your app must queue any tracking events that arrive between the [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) and its response. When the Sessions response arrives, you should first process any queued [events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md), then you can start processing _live_ events with the [Events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) calls.

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
