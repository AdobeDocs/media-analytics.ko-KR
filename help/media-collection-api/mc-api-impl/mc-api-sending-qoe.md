---
title: QoE 데이터 보내기
description: qoeData JSON 키로 이벤트 전송에 대해 알아봅니다.
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '57'
ht-degree: 84%

---

# QoE 데이터 보내기{#sending-qoe-data}

모든 이벤트는 JSON 요청 본문에서 `qoeData` 키와 함께 배치되는 `params`라는 추가 JSON 키로 데코레이트할 수 있습니다.

>[!NOTE]
>
>매개 변수 유형을 [JSON 유효성 검사 스키마](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)에서 확인하고 이러한 유형이 필수인지 아니면 선택 사항인지 확인해야 합니다.
