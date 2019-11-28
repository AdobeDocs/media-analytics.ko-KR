---
title: 구현 경로
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 구현 경로 {#implementation-paths}

Media Analytics(하트비트)는 Adobe의 표준화된 비디오 솔루션입니다. Adobe의 이전 이정표 모델을 대체했습니다.

이러한 각 구현 경로의 경우 Media Analytics는 고유한 SKU를 포함하며, 서버 호출을 기반으로 한 가격 책정 모델에서 비디오 스트림을 기반으로 한 모델로 변경되기 때문에 고객이 영업 담당자/계정 관리자에게 연락하여 새 판매 주문에 서명하도록 요청해야 합니다.

* **고객측 -** Media Analytics 전용 통합입니다. 비디오 하트비트 SDK 및/또는 Media Collection API 통합을 선택할 수 있습니다. 이 경로는 Brightcove, Ooyala, thePlatform 등과 같은 고객 및/또는 OVP 플레이어를 포함한 모든 비디오 플레이어에서 사용할 수 있습니다.

   Media Analytics가 의도한 경로인 경우 [Media SDK 구현](/help/sdk-implement/setup/setup-overview.md) 및 [Media Collection API](/help/media-collection-api/mc-api-overview.md)를 참조하십시오.

   >[!IMPORTANT]
   >
   >Media Analytics를 사용하려면 고객이 Adobe Analytics도 사용해야 합니다.

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch는 Dynamic Tag Management의 후속 제품으로서, 플레이어에서 비디오 추적 기능을 간편하게 구현할 수 있도록 해주는 Media Analytics Launch 확장 기능을 제공합니다.

   Experience Platform Launch에 대한 자세한 내용은 [Adobe Media Analytics for Audio 및 Video 확장](https://docs.adobe.com/content/help/ko-KR/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)에서 확인할 수 있습니다.
* **Adobe Primetime -** Adobe Primetime은 컨텐츠 프로그래머 및 배포자가 연결된 모든 화면에서 미디어를 이용하여 수익을 창출할 수 있도록 지원하는 Adobe Experience Cloud 솔루션입니다.

   Primetime은 비디오 게시, 광고, 개인화 및 분석에 필요한 모듈식 플랫폼을 제공하여 장치 간 글로벌 대상의 접근성, 수익성 및 활성화를 용이하게 합니다. 또한 Primetime은 다음과 같은 솔루션 및 값을 제공합니다.

   * 선형 및 VOD 컨텐츠 유형을 정확하게 측정할 수 있도록 지원합니다.
   * 동적 광고 삽입을 포함하거나 포함하지 않고 광고 브레이크 측정을 지원합니다.
   * TVSDK의 원활한 광고 삽입 모델을 통해 광고 재생을 직접 측정하는 분석이 가능하므로 정확도가 높아집니다.
   * 모바일에서의 QoS 버퍼링 또는 모바일 연결 중단 문제와 최종 사용자 상호 작용(예: 찾기, 일시 정지, 백그라운드 작업)의 정확성을 보장하기 위한 강력한 이벤트 및 메타데이터 세트입니다.
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK는 이미 Media Analtyics(하트비트) SDK에 통합되었으므로 지원되는 모든 플랫폼에서 훨씬 쉽고 빠르게 구현할 수 있습니다. <!--Primetime also supports the partnership with Nielsen.--> Primetime을 활용하려면 플랫폼용 문서인 [Primetime 사용 안내서](https://helpx.adobe.com/kr/primetime/user-guide.html)와 함께 [클라이언트측](/help/intro-to-ava/implementation-paths/client-side-path.md)에서 제공하는 동일한 지침 및 사전 요구 사항을 따르십시오.

또한 영업 담당자/계정 관리자에게 문의하여 TVSDK를 구입하기 위해 해야 할 작업에 대해 논의해야 합니다.
