---
title: 세션 ID 가져오기
description: 응답의 위치 헤더에서 세션 ID를 얻기 위해 세션 요청을 코딩하는 방법을 알아봅니다.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 69%

---

# 세션 ID 가져오기{#obtaining-a-session-id}

참조 플레이어의 이 코드 조각은 응답의 위치 헤더에서 세션 ID(및 Media Collection API 버전) 추출과 함께 [세션 요청](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)을 코딩하는 방법을 보여 줍니다.

```js
var  
sessionData = { 
        ... 
        "media.contentType": "VOD", 
        "media.channel": "sample-channel", 
        ... 
    } 
}; 
...

const SESSION_ID_EXTRACTOR = /^\/api\/(.*)\/sessions\/(.*)/; 
    ...
    apiClient.request({ 
        "baseUrl": config.apiBaseUrl,   // The endpoint 
        "path": config.apiSessionsPath, // api/v1/sessions/ 
        "method": "POST",               // (Always POST) 
        "data": sessionData             // Mandatory params 
     }).then((response) => { 
        // Extract Session ID (and API version) 
        const [, apiVersion, sessionId] =  response.headers.Location.match(SESSION_ID_EXTRACTOR);  
        this.sessionId = sessionId;     // Session ID obtained 
        this._sessionStarted = true;    // Session started. 
    ...
```
