---
title: Streaming Media에 대한 사전 요구 사항에 대해 알아봅니다.
description: 스트리밍 미디어용 Adobe Analytics를 시작합니다. 스트리밍 미디어용 Adobe Analytics을 구현하기 위해 필요한 사항을 알아봅니다.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 74%

---

# 사전 요구 사항 {#prerequisites}

스트리밍 미디어 구현을 시작하기 전에 다음 작업을 완료하십시오.

1. **스트리밍 미디어 개요 검토**<br>
Streaming Media 구현을 시작하기 전에 [Streaming Media 개요](/help/media-overview.md) Streaming Media가 사용자의 요구 사항을 충족하는지 확인합니다.

1. **Steaming Media 가격 책정 모델 확인**<br>
현재 가격 책정 모델은 비디오 스트림을 기반으로 합니다. 스트리밍 미디어는 Adobe Analytics의 추가 기능으로 별도로 판매되므로 필요한 경우 영업 담당자 또는 Adobe 계정 팀에 문의하십시오.<!--update when media SKUs are added to other AEP apps -->

1. **Adobe Analytics 보고서 활성화**<br>
Analytics에서 보고서를 활성화하고 수집 중인 콘텐츠 및 광고 데이터를 보려면 Analytics에서 보고서를 활성화해야 합니다. [미디어 보고서 지원](/help/reporting/media-reports-enable.md)을 확인하십시오.

1. **Experience Cloud에서 Adobe Experience Platform ID 서비스 구현**

   **ID 서비스**&#x200B;를 통해 사용자 핵심 서비스의 Experience Cloud 핵심 서비스, 솔루션, 고객 속성 및 대상자에 공통된 ID 프레임워크를 사용할 수 있습니다. 이 서비스는 영구적인 고유 ID를 사이트 방문자에게 할당하여 작동됩니다. 조직이 ID 서비스를 구현하면 이 ID를 사용하여 다른 Experience Cloud 솔루션에서 동일한 사이트 방문자와 해당 데이터를 식별할 수 있습니다.

   ![ID 서비스 그래픽](assets/mc_id_service_graphic.png)

   ID 서비스는 다른 솔루션별 ID(예: Analytics AID)를 대체할 수도 있습니다. ID 서비스에서는 [고객 ID 및 인증 상태](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=ko-KR) 기능을 통해 고유한 고객 ID를 Experience Cloud에 전달할 수 있습니다. 단, ID 서비스는 이미 구독한 솔루션에서만 작동한다는 점을 잊지 마십시오. 다른 제품에 액세스할 수 있도록 등록하지 않았다면 ID 서비스에서는 액세스 권한을 제공하지 않습니다.

   ID 서비스는 대부분의 Experience Cloud 기능, 개선 사항 및 서비스에 대한 필수 구성 요소입니다. 현재 ID 서비스는 [Analytics](https://www.adobe.com/kr/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/kr/marketing-cloud/data-management-platform.html) 및 [Target](https://www.adobe.com/kr/marketing-cloud/testing-targeting.html)을 지원합니다.

   ID 서비스를 구현하지 않았다면 지금이 바로 마이그레이션 전략을 시작할 적기입니다. ID 서비스의 중요성과 역할에 대한 자세한 내용은 [Identity 서비스가 나의 레이더가 되어야 하는 이유](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)를 참조하십시오.

   Experience Cloud ID에 대한 자세한 내용은 [Experience Cloud ID 개요](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) 및 [Adobe Experience Platform ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/home.html)를 참조하십시오.

1. **구현 방법에 대한 추가 전제 조건 보기**

   스트리밍 미디어를 구현하는 방법에 따라 다음 구현 방법 중 하나에 대한 사전 요구 사항을 확인합니다.

   * [Adobe Analytics 전용 구현을 위한 사전 요구 사항](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Edge 구현을 위한 사전 요구 사항](/help/implementation/edge/prerequisites-edge.md)

   사용 [구현 개요](/help/implementation/overview.md) 적합한 구현 방법을 결정하십시오.
