---
title: 플레이어에서 HTTP 요청 유형 설정
description: 플레이어에서 HTTP 요청 유형 설정
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 100%

---

# HTTP 요청 유형 설정 {#setting-the-http-request-type}

모든 Media Collection API 요청에 대한 요청 본문은 JSON 형식이어야 하므로 플레이어에서 컨텐츠 요청 유형을 설정해야 합니다. 예를 들어, JavaScript에서 `Content-Type`요청 헤더를 다음과 같이 설정합니다.

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
