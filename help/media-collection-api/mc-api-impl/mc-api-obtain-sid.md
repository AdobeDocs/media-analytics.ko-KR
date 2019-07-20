---
seo-title: 세션 ID 가져오기
title: 세션 ID 가져오기
uuid: fc 8712 fa -848 f -4564-af 5 d -5 dd 9 d 6 b 088 d 8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# 세션 ID 가져오기{#obtaining-a-session-id}

This code snippet from the Reference Player shows one way of coding a [Sessions request,](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) along with extracting the Session ID (and the Media Collection API version) from the Location header in the response:

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

