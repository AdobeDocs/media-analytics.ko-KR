---
seo-title: 플레이어에서 HTTP 요청 유형 설정
title: 플레이어에서 HTTP 요청 유형 설정
uuid: b8fa7233-e654-4acf-a9d7-14158cde13e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# Setting the HTTP request type {#setting-the-http-request-type}

모든 Media Collection API 요청에 대한 요청 본문은 JSON 형식이어야 하므로 플레이어에서 컨텐츠 요청 유형을 설정해야 합니다. For example, in JavaScript you would set the `Content-Type` request header as follows:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

