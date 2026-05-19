---
title: 스트리밍 미디어 서비스 JSON 유효성 검사 스키마
description: Streaming Media JSON 유효성 검사 스키마의 정의 및 각 이벤트 유형에 대한 올바른 요청 본문 매개 변수를 결정하기 위해 사용되는 방법.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ZWKv1LJKc8qLkZYpcNdDFEs8Er70toRCoufarMcgVKQ
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
source-wordcount: 84
ht-degree: 71%

---

# JSON 유효성 검사 스키마{#json-validation-schemas}

스트리밍 미디어 컬렉션 백 엔드는 JSON 유효성 검사 스키마를 사용하여 각 이벤트 유형에 대한 요청 매개 변수의 유효성을 검사합니다. 이러한 스키마는 사용자가 사용할 수 있으며, MA API에 사용된 매개 변수 유형에 대한 현재 권한으로 사용됩니다.

`GET https://{uri}/api/v1/schemas/{event-type}`

JSON 유효성 검사 스키마 사용 방법에 대한 자세한 내용은 [이벤트 요청 확인](../mc-api-impl/mc-api-validate-reqs.md)을 참조하십시오.
