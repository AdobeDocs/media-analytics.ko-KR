---
title: 전제 조건
description: null
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 전제 조건{#prerequisites}

## 의사 결정 {#decision}

추적 구현을 시작하기 전에 사용자의 상황에 가장 적합한 구현에 대해 몇 가지 결정을 미리 내려야 합니다.

* **Media Analytics -** 최신 Media SDK(표준, 권장 구현) 및/또는 Media Collection API(RESTful) 사용
* **이정표 -** 이전의 Adobe 추적 구현
* **Data Insertion API -** Media SDK를 사용하지 않고 추적 구현

## 작업 {#prereq-tasks}

Media *Analytics* 구현의 경우 시작하기 전에 완료해야 하는 작업은 다음과 같습니다.

1. **Experience Cloud를 사용할 수 있도록 설정.**

   Adobe Experience Platform ID 서비스를 구현해야 합니다.

    Identity 서비스를 통해 사용자 핵심 서비스의 Experience Cloud 핵심 서비스, 솔루션, 고객 속성 및 대상에 공통된 ID 프레임워크를 사용할 수 있습니다. 이는 영구적인 고유 ID를 사이트 방문자에게 할당하여 작동됩니다. 조직에서 ID 서비스를 구현하면 이 ID를 통해 다른 Experience Cloud 솔루션에서 동일한 사이트 방문자와 해당 데이터를 식별할 수 있습니다.

   ![](assets/mc_id_service_graphic.png)

   ID 서비스는 다른 솔루션별 ID(예: Analytics AID)를 대체할 수도 있습니다. [고객 ID 및 인증 상태](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-authenticated-state.html) 기능을 통해 ID 서비스를 사용하여 고유한 고객 ID를 Experience Cloud에 전달할 수 있습니다. 하지만 ID 서비스는 이미 구독한 솔루션에서만 작동합니다. 다른 제품에 액세스하기 위해 등록되어 있지 않은 경우 ID 서비스를 통해 액세스할 수 없습니다.

   나아가 ID 서비스는 현재 및 미래의 수 많은 Experience Cloud 기능, 개선 사항 및 서비스의 필수 구성 요소입니다. Currently, the ID service supports [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) and [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Adobe Experience Cloud Device Co-op에 참여하려면 Experience Cloud ID 서비스가 필요합니다.

   ID 서비스를 구현하지 않았다면 지금이 바로 마이그레이션 전략을 시작할 적기입니다. For more information about the importance and role of the ID service, see [Why the Identity Service Should be on Your Radar.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >In the absence of any user ID information present on the media-specific calls, the default analytics [Fallback ID Methods](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) will apply.

   For additional information about the Experience Cloud ID, see [Experience Cloud ID Overview,](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) and [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/)

1. **Adobe Analytics 보고서를 사용할 수 있도록 설정.**

   To enable reports in Analytics and see the content and ad data you are collecting, see [Media reports enablement.](/help/media-reports/media-reports-enable.md)

