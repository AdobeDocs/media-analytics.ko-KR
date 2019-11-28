---
title: 플레이어에서 HTTP 요청 유형 설정
description: null
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# HTTP 요청 유형 설정 {#setting-the-http-request-type}

모든 Media Collection API 요청에 대한 요청 본문은 JSON 형식이어야 하므로 플레이어에서 컨텐츠 요청 유형을 설정해야 합니다. 예를 들어, JavaScript에서 `Content-Type`요청 헤더를 다음과 같이 설정합니다.

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

