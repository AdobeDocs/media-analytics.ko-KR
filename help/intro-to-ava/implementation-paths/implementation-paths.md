---
title: 어떤 스트리밍 미디어 구현 경로를 사용할 수 있습니까?
description: Adobe Launch를 포함한 Adobe 스트리밍 미디어 구현 경로에 대해 알아보십시오.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 100%

---

# 구현 경로 {#implementation-paths}

이 구현 경로의 경우 스트리밍 미디어 Analytics는 고유한 SKU를 포함하며, 서버 호출을 기반으로 한 가격 책정 모델에서 비디오 스트림을 기반으로 한 모델로 변경되기 때문에 고객이 영업 담당자/계정 관리자에게 연락하여 새 판매 주문에 서명해야 합니다.

* **Adobe Media Analytics 확장이 있는 Adobe Launch**

   Adobe Launch는 Adobe의 차세대 tag management 솔루션입니다. Launch는 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 제공합니다. Launch와의 자체 통합을 구축하고 유지 관리하기 위해 확장을 사용합니다. 확장은 Launch UI 및 클라이언트 기능을 확장하는 JavaScript, HTML 및 CSS 패키지입니다. 자세한 내용은 [Experience Platform Launch 사용 안내서](https://experienceleague.adobe.com/docs/launch/using/overview.html?lang=kr)를 참조하십시오.

   Adobe Media Analytics(MA) 확장은 오디오 및 비디오를 위한 핵심 JavaScript Media SDK(Media 2.x SDK)를 추가합니다. 이 확장은 Launch 사이트 또는 프로젝트에 `MediaHeartbeat` 추적기 인스턴스를 추가하는 기능을 제공합니다.

   Media Analytics 확장을 사용하는 Adobe Launch를 사용하려면 다음 사항을 충족해야 합니다.
   * Adobe Experience Cloud 고객이어야 합니다.
   * 웹 페이지에 Launch 또는 DTM 포함 코드를 배포해야 합니다.
   * [Analytics 확장](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html?lang=kr)
   * [Experience Cloud ID 확장](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html?lang=kr)


* **고객측 -** Media Analytics 전용 통합입니다. 비디오 하트비트 SDK 및/또는 Media Collection API 통합을 선택할 수 있습니다. 이 경로는 Brightcove, Ooyala, thePlatform 등과 같은 고객 및/또는 OVP 플레이어를 포함한 모든 비디오 플레이어에서 사용할 수 있습니다.

   Media Analytics가 의도한 경로인 경우 [Media SDK 구현](/help/sdk-implement/setup/setup-overview.md) 및 [Media Collection API](/help/media-collection-api/mc-api-overview.md)를 참조하십시오.

   >[!IMPORTANT]
   >
   >Media Analytics를 사용하려면 고객이 Adobe Analytics도 사용해야 합니다.

* **Adobe Primetime -** Adobe Primetime은 컨텐츠 프로그래머 및 배포자가 연결된 모든 화면에서 미디어를 이용하여 수익을 창출할 수 있도록 지원하는 Adobe Experience Cloud 솔루션입니다.

   Primetime은 비디오 게시, 광고, 개인화 및 분석에 필요한 모듈식 플랫폼을 제공하여 장치 간 글로벌 대상의 접근성, 수익성 및 활성화를 용이하게 합니다. 또한 Primetime은 다음과 같은 솔루션과 가치를 제공합니다.

   * 선형 및 VOD 컨텐츠 유형을 정확하게 측정할 수 있도록 지원합니다.
   * 동적 광고가 삽입된(또는 삽입되지 않은) 광고 브레이크를 측정할 수 있도록 지원합니다.
   * TVSDK의 매끄러운 광고 삽입 모델을 사용하면 광고 재생을 직접 측정하는 분석을 통해 정확도를 높일 수 있습니다.
   * QoS 버퍼링 또는 모바일 연결 중단 문제와 모바일에서 검색, 일시 정지 및 백그라운드 실행과 같은 최종 사용자 상호 작용에서 정확성을 보장하는 강력한 이벤트 및 메타데이터 집합.

<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK는 이미 Media Analtyics(하트비트) SDK에 통합되었으므로 지원되는 모든 플랫폼에서 훨씬 쉽고 빠르게 구현할 수 있습니다. <!--Primetime also supports the partnership with Nielsen.--> Primetime을 활용하려면 플랫폼용 문서인 [Primetime 사용 안내서](https://helpx.adobe.com/kr/primetime/user-guide.html)와 함께 [클라이언트측](/help/intro-to-ava/implementation-paths/client-side-path.md)에서 제공하는 동일한 지침 및 사전 요구 사항을 따르십시오.

또한 영업 담당자/계정 관리자에게 문의하여 TVSDK를 구입하기 위해 해야 할 작업에 대해 논의해야 합니다.
