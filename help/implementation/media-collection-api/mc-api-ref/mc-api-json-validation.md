---
title: 스트리밍 미디어 컬렉션 JSON 유효성 검사 스키마
description: Streaming Media JSON 유효성 검사 스키마의 정의 및 각 이벤트 유형에 대한 올바른 요청 본문 매개 변수를 결정하기 위해 사용되는 방법.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 72%

---

# JSON 유효성 검사 스키마{#json-validation-schemas}

스트리밍 미디어 컬렉션 백 엔드는 JSON 유효성 검사 스키마를 사용하여 각 이벤트 유형에 대한 요청 매개 변수의 유효성을 검사합니다. 이러한 스키마는 사용자가 사용할 수 있으며, MA API에 사용된 매개 변수 유형에 대한 현재 권한으로 사용됩니다.

`GET https://{uri}/api/v1/schemas/{event-type}`

JSON 유효성 검사 스키마 사용 방법에 대한 자세한 내용은 [이벤트 요청 확인](../mc-api-impl/mc-api-validate-reqs.md)을 참조하십시오.
