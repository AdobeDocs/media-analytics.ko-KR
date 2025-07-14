---
title: 어떤 Streaming Media 구현 경로를 사용할 수 있습니까?
description: Adobe Experience Platform 데이터 수집을 포함한 Adobe Streaming Media 구현 경로에 대해 알아보십시오.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 92%

---

# 구현 경로 {#implementation-paths}

**이 콘텐츠는 현재 구현 경로 파일**&#x200B;로 이동되었습니다.

스트리밍 미디어용 Analytics는 고유한 SKU를 포함하며, 서버 호출을 기반으로 한 가격 책정 모델에서 비디오 스트림을 기반으로 한 모델로 변경되기 때문에 각 구현 경로의 경우 고객이 영업 담당자/Adobe 계정 팀에 연락하여 새 판매 주문에 서명해야 합니다.

## Adobe Media Analytics 확장을 통한 Adobe Experience Platform 데이터 수집

>[!NOTE]
>Adobe Experience Platform Launch는 Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=ko)를 참조하십시오.


Adobe Experience Platform의 태그는 Adobe의 차세대 태그 관리 기능입니다. 태그를 통해 관련 고객 경험을 강화하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 고 관리하는 간단한 방법을 고객에게 제공합니다. 태그는 포함된 부가 가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다.

태그는 확장이라고 하는 자체 통합을 구축하고 유지할 수 있는 권한을 누구에게나 부여합니다. Adobe Experience Cloud 고객은 앱 스토어 환경에서 이러한 확장을 사용할 수 있으므로 태그를 신속하게 설치, 구성 및 배포할 수 있습니다.

확장은 태그 기능을 확장하는 코드 패키지(JavaScript, HTML 및 CSS)입니다. 사실상의 셀프서비스 인터페이스를 사용하여 통합을 구축, 관리 및 업데이트합니다. 확장은 작업을 수행하는 데 사용하는 앱으로 간주할 수 있습니다. 자세한 내용은 [Adobe Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)의 *태그 개요* 문서를 참조하십시오.

Adobe Media Analytics(MA) 확장은 오디오 및 비디오를 위한 핵심 JavaScript Media SDK(Media 2.x SDK)를 추가합니다. 이 확장은 데이터 수집 사이트 또는 프로젝트에 `MediaHeartbeat` 추적기 인스턴스를 추가하는 기능을 제공합니다.

Media Analytics 확장이 포함된 Adobe 데이터 수집을 사용하려면 다음 사항을 충족해야 합니다.
* Adobe Experience Cloud 고객이어야 합니다.
* 웹 페이지에 데이터 수집 또는 DTM 임베드 코드를 배포해야 합니다.
* [Analytics 확장 기능](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=ko)
* [Experience Cloud ID 확장 기능](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=ko)


## 클라이언트측

Media Analytics 전용 통합입니다. 비디오 하트비트 SDK 및/또는 Media Collection API 통합을 선택할 수 있습니다. 이 경로는 Brightcove, Ooyala, thePlatform 등과 같은 고객 및/또는 OVP 플레이어를 포함한 모든 비디오 플레이어에서 사용할 수 있습니다.

Media Analytics가 의도한 경로인 경우 [Media SDK 구현](/help/legacy/setup/legacy-setup-overview.md) 및 [Media Collection API](/help/implementation/media-collection-api/mc-api-overview.md)를 참조하십시오.

>[!IMPORTANT]
>Media Analytics를 사용하려면 고객이 Adobe Analytics도 사용해야 합니다.

## Adobe Primetime

Adobe Primetime은 콘텐츠 프로그래머 및 배포자가 연결된 모든 화면에서 미디어를 이용하여 수익을 창출할 수 있도록 지원하는 Adobe Experience Cloud 솔루션입니다.

Primetime은 비디오 게시, 광고, 개인화 및 분석에 필요한 모듈식 플랫폼을 제공하여 디바이스 간 글로벌 대상자의 접근성, 수익성 및 활성화를 용이하게 합니다. 또한 Primetime은 다음과 같은 솔루션과 가치를 제공합니다.

* 선형 및 VOD 콘텐츠 유형을 정확하게 측정할 수 있도록 지원합니다.
* 동적 광고가 삽입된(또는 삽입되지 않은) 광고 브레이크를 측정할 수 있도록 지원합니다.
* TVSDK의 매끄러운 광고 삽입 모델을 사용하면 광고 재생을 직접 측정하는 분석을 통해 정확도를 높일 수 있습니다.
* QoS 버퍼링 또는 모바일 연결 중단 문제와 모바일에서 검색, 일시 정지 및 백그라운드 실행과 같은 최종 사용자 상호 작용에서 정확성을 보장하는 강력한 이벤트 및 메타데이터 집합.
* Nielsen DTVR(선형)과 ID3 메타데이터 통합 및 DCR과 CMS 메타데이터 통합을 지원합니다.


TVSDK는 이미 Media Analtyics(하트비트) SDK에 통합되었으므로 지원되는 모든 플랫폼에서 훨씬 쉽고 빠르게 구현할 수 있습니다. Primetime을 활용하려면 플랫폼용 문서인 [Primetime 사용 안내서](/help/legacy/intro-to-ava/implementation-paths/client-side-path.md)와 함께 [클라이언트측](https://helpx.adobe.com/primetime/user-guide.html)에서 제공하는 동일한 지침 및 사전 요구 사항을 따르십시오.

또한 영업 담당자/계정 관리자에게 문의하여 TVSDK를 구입하기 위해 해야 할 작업에 대해 논의해야 합니다.
