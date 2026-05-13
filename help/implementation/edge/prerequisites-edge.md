---
title: Adobe Analytics 전용 구현을 위한 사전 요구 사항
description: Adobe Analytics 전용 구현 또는 Edge 구현과 함께 스트리밍 미디어 컬렉션을 사용하기 위한 사전 요구 사항에 대해 알아봅니다
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
TQID: https://experienceleague.adobe.com/OqimGafihuirpnAaZ4AvrX2lrOmCtr0FLXk3QwoVTew
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 212
ht-degree: 16%

---

# Edge 구현을 위한 사전 요구 사항

이 섹션에 설명된 사전 요구 사항은 Edge 구현을 통해 Adobe 스트리밍 미디어 컬렉션을 구현하는 것입니다.

1. **일반 필수 구성 요소를 완료하십시오.**<br>
Adobe Analytics 전용 구현용 또는 Edge 구현용 Streaming Media Collection을 구현하는지 여부에 관계없이 [일반 사전 요구 사항](/help/getting-started/prereqs.md)을 충족하는지 확인하십시오.

1. **Edge Network 및 Streaming Media Collection과 호환되는 Adobe 솔루션을 구현하고 있는지 확인**<br>
Edge을 사용하여 스트리밍 미디어 컬렉션을 구현하는 경우 작동하는 Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer 또는 Real-Time Customer Data Platform 구현도 있어야 합니다. 자세한 내용은 다음 설명서 리소스를 참조하십시오.
   * [Customer Journey Analytics 안내서](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=ko)
   * [Adobe Analytics 구현](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
   * [Adobe Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ko)
   * [Real-Time Customer Data Platform 설명서](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **미디어 추적 서버 URL 가져오기**<br>
미디어 추적 서버 URL은 Customer Journey Analytics 담당자에게 문의하십시오. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Edge Network을 사용하여 스트리밍 미디어 컬렉션 구현**<br>
[Edge Network을 사용하여 스트리밍 미디어 컬렉션 구현](/help/implementation/edge/implementation-edge.md)의 단계를 따릅니다.
