---
title: 플레이어에서 HTTP 요청 유형 설정
description: 모든 Media Collection API 요청에 대한 요청 본문은 JSON 형식이어야 합니다. 플레이어에서 콘텐츠 요청 유형을 설정하는 방법에 대해 알아봅니다.
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 81%

---

# HTTP 요청 유형 설정 {#setting-the-http-request-type}

모든 Media Collection API 요청에 대한 요청 본문은 JSON 형식이어야 하므로 플레이어에서 콘텐츠 요청 유형을 설정해야 합니다. 예를 들어, JavaScript에서 `Content-Type`요청 헤더를 다음과 같이 설정합니다.

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
