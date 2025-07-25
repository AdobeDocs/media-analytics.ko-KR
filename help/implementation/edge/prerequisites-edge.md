---
title: Adobe Analytics 전용 구현을 위한 사전 요구 사항
description: Adobe Analytics 전용 구현 또는 Edge 구현과 함께 스트리밍 미디어 컬렉션을 사용하기 위한 사전 요구 사항에 대해 알아봅니다
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 0b0b4a373b15191dcb37dc436413f68cdc70768e
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 10%

---

# Edge 구현을 위한 사전 요구 사항

이 섹션에 설명된 사전 요구 사항은 Edge 구현을 통해 Adobe 스트리밍 미디어 컬렉션을 구현하는 것입니다.

1. **일반 필수 구성 요소를 완료합니다**<br>
Adobe Analytics 전용 구현용 또는 Edge 구현용 Streaming Media Collection을 구현하는지 여부에 관계없이 [일반 사전 요구 사항](/help/getting-started/prereqs.md)을 충족하는지 확인하십시오.

1. **Edge Network 및 스트리밍 미디어 컬렉션과 호환되는 Adobe 솔루션을 구현하고 있는지 확인**<br>
Edge을 사용하여 스트리밍 미디어 컬렉션을 구현하는 경우 작동하는 Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer 또는 Real-Time Customer Data Platform 구현도 있어야 합니다. 자세한 내용은 다음 설명서 리소스를 참조하십시오.
   * [Customer Journey Analytics 안내서](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=ko)
   * [Adobe Analytics 구현](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ko)
   * [Adobe Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ko)
   * [Real-Time Customer Data Platform 설명서](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=ko)

1. **미디어 추적 서버 URL 가져오기**<br>
미디어 추적 서버 URL은 Customer Journey Analytics 담당자에게 문의하십시오. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Edge Network을 사용하여 스트리밍 미디어 컬렉션 구현**<br>
[Edge Network을 사용하여 스트리밍 미디어 컬렉션 구현](/help/implementation/edge/implementation-edge.md)의 단계를 따릅니다.
