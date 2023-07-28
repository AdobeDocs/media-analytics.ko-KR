---
title: Adobe Analytics 전용 구현을 위한 사전 요구 사항
description: Adobe Analytics 전용 구현에 스트리밍 미디어를 사용하기 위한 사전 요구 사항에 대해 알아봅니다
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 13%

---

# Edge 구현을 위한 사전 요구 사항

이 섹션에 설명된 사전 요구 사항은 Edge 구현을 통해 Streaming Media를 구현하는 것입니다.

1. **일반 사전 요구 사항 완료**<br>
Adobe Analytics 전용 구현용 Streaming Media를 구현하든 Edge 구현용 Streaming Media를 구현하든 다음을 충족하는지 확인합니다. [일반 사전 요구 사항](/help/getting-started/prereqs.md).

1. **Edge 및 스트리밍 미디어와 호환되는 Adobe 솔루션을 구현하고 있는지 확인합니다.**<br>
Edge를 사용하여 스트리밍 미디어를 구현할 때 작업 Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer 또는 Real-time Customer Data Platform 구현도 있어야 합니다. 자세한 내용은 다음 설명서 리소스를 참조하십시오.
   * [Customer Journey Analytics 안내서](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=ko-KR)
   * [Adobe Analytics 구현](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
   * [Adobe Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ko)
   * [Real-time Customer Data Platform 설명서](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **미디어 추적 서버 URL 얻기**<br>
미디어 추적 서버 URL은 Customer Journey Analytics 담당자에게 문의하십시오. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Edge로 Media Analytics 설치**<br>
의 단계를 따릅니다. [Experience Platform Edge로 Media Analytics 설치](/help/implementation/edge/implementation-edge.md).