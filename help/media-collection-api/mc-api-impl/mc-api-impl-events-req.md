---
title: 이벤트 요청 구현
description: 세션 ID를 가져온 후 모든 후속 추적 호출에 이벤트 요청 종단점을 사용하는 방법을 알아봅니다
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 80%

---

# 이벤트 요청 구현{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

다음 작업을 사용하여 세션 ID를 가져온 이후 모든 후속 추적 호출에 [이벤트 요청](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) 사용: [세션 요청](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) 포함하려는 선택적 매개 변수, 플레이헤드 위치 및 타임스탬프, 이벤트 유형을 JSON 요청 본문에 지정합니다.

세션 요청의 본문 구조와 [이벤트 요청](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)에 대한 JSON 요청 본문의 구조는 동일하지만, [JSON 유효성 검사 스키마](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)에서 매개 변수 요구 사항 및 유형을 확인합니다.
