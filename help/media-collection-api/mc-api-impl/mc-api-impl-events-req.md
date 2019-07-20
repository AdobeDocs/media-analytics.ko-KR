---
seo-title: 이벤트 요청 구현
title: 이벤트 요청 구현
uuid: 3 BFA 313 C-FF 74-4 E 2 E-BBDE -6 F 4 A 6221 D 85 B
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# 이벤트 요청 구현{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use the [Events request](../../media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [Sessions request.](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) 요청의 JSON 본문에 재생 헤드 위치 및 타임스탬프, 이벤트 유형 및 포함할 선택적 매개 변수를 지정합니다.

[이벤트 요청의](../../media-collection-api/mc-api-ref/mc-api-events-req.md) JSON 요청 본문은 세션 요청의 구조와 동일하지만 매개 변수 요구 사항 및 유형에 대한 [JSON 유효성 검사 스키마를](../../media-collection-api/mc-api-ref/mc-api-json-validation.md) 확인합니다.
