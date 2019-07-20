---
seo-title: 구현 경로
title: 구현 경로
uuid: 8400 c 938-E 77 E -4 c 88-B 23 B -5 F 5977 A 5316 C
translation-type: tm+mt
source-git-commit: ca7e63d9af1f84c7d5d620c72df5f62555f68c03

---


# 구현 경로 {#implementation-paths}

미디어 분석 (하트 비트) 는 Adobe의 표준 비디오 솔루션입니다. Adobe의 이전 이정표 모델을 대체했습니다.

이러한 구현 경로 각각에 대해, 미디어 분석으로 새 판매 주문에 서명하려면 고객 영업 담당자에게 연락하여 미디어 스트림에 기반한 모델에 대한 서버 호출을 기반으로 가격 모델에서 가격 모델을 변경해야 합니다.

* **클라이언트측 -** 미디어 분석 전용 통합입니다. 비디오 하트비트 SDK 및/또는 Media Collection API 통합을 선택할 수 있습니다. 이 경로는 Brightcove, Ooyala, thePlatform 등과 같은 고객 및/또는 OVP 플레이어를 포함한 모든 비디오 플레이어에서 사용할 수 있습니다.

   If Media Analytics is your intended path, see the [Media SDK Implementation](../../sdk-implement/setup/setup-overview.md) and the [Media Collection API.](../../media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >미디어 분석을 사용하려면 Adobe Analytics도 사용해야 합니다.

* **Adobe Experience Platform Launch -** 다이내믹 태그 관리에 대한 후속 제품인 Adobe Experience Platform Launch는 플레이어에서 비디오 추적을 구현하는 미디어 분석 런칭 익스텐션을 제공합니다.

   You can learn more about Experience Platform Launch here: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime -** Adobe Primetime는 컨텐츠 프로그래머 및 배포업체가 연결된 모든 화면에서 미디어를 상용화할 수 있는 Adobe Experience Cloud 솔루션입니다.

   Primetime은 비디오 게시, 광고, 개인화 및 분석에 필요한 모듈식 플랫폼을 제공하여 장치 간 글로벌 대상의 접근성, 수익성 및 활성화를 용이하게 합니다. 또한 Primetime은 다음과 같은 솔루션 및 값을 제공합니다.

   * 선형 및 VOD 컨텐츠 유형을 정확하게 측정할 수 있도록 지원합니다.
   * 동적 광고 삽입을 포함하거나 포함하지 않고 광고 브레이크 측정을 지원합니다.
   * TVSDK의 원활한 광고 삽입 모델을 통해 광고 재생을 직접 측정하는 분석이 가능하므로 정확도가 높아집니다.
   * 모바일에서의 QoS 버퍼링 또는 모바일 연결 중단 문제와 최종 사용자 상호 작용(예: 찾기, 일시 정지, 백그라운드 작업)의 정확성을 보장하기 위한 강력한 이벤트 및 메타데이터 세트입니다.
   * Nielsen DTVR(선형)과 ID3 메타데이터 통합 및 DCR과 CMS 메타데이터 통합을 지원합니다.
   TVSDK는 이미 미디어 맬웨어 (하트 비트) SDK와 통합되어 있으므로 지원되는 모든 플랫폼에서 훨씬 쉽고 빠르게 구현할 수 있습니다. Primetime은 또한 Nielsen과 파트너십을 지원합니다. Primetime을 활용하려면 현재 플랫폼에 대한 다음 문서와 함께 [고객측](../../intro-to-ava/implementation-paths/client-side-path.md)에 나와 있는 것과 동일한 지침 및 사전 요구 사항을 따르십시오. [Primetime 사용 안내서.](https://helpx.adobe.com/primetime/user-guide.html)

   또한 영업 담당자/계정 관리자에게 문의하여 TVSDK를 구입하기 위해 해야 할 작업에 대해 논의해야 합니다.
