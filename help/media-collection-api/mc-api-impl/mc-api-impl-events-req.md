---
title: 이벤트 요청 구현
description: null
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 이벤트 요청 구현{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

세션 ID를 [세션 요청을 사용하여 가져온 이후의 모든 후속 추적 호출에는 [이벤트 요청](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)을 사용합니다.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) 포함하려는 선택적 매개 변수, 플레이헤드 위치 및 타임스탬프, 이벤트 유형을 JSON 요청 본문에 지정합니다.

세션 요청의 본문 구조와 [이벤트 요청](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)에 대한 JSON 요청 본문의 구조는 동일하지만, [JSON 유효성 검사 스키마](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)에서 매개 변수 요구 사항 및 유형을 확인합니다.
