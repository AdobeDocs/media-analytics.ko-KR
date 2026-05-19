---
title: 세션 ID 가져오기
description: 응답의 위치 헤더에서 세션 ID를 가져오기 위해 세션 요청을 코딩하는 방법에 대해 알아봅니다.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/GmrgXTVz-ncVomHD5z2dfXo8N8e9WWU6CJmPNqsMYag
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 61
ht-degree: 100%

---

# 세션 ID 가져오기{#obtaining-a-session-id}

참조 플레이어의 이 코드 조각은 응답의 위치 헤더에서 세션 ID(및 Media Collection API 버전) 추출과 함께 [세션 요청](../mc-api-ref/mc-api-sessions-req.md)을 코딩하는 방법을 보여 줍니다.

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
