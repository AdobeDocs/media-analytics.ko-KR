---
title: 시작하기
description: 스트리밍 미디어용 Adobe Analytics를 시작합니다.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: 8b939da2374acb5d573a553c848ba880345e64b5
workflow-type: ht
source-wordcount: '439'
ht-degree: 100%

---

# 시작하기 {#getting-started}

스트리밍 미디어용 Adobe Analytics는 Media SDK와 Media Collection API, 이렇게 두 가지 주요 구현 방법을 제공합니다.

![방법](assets/getting-started2.png)

**Media SDK**&#x200B;의 기본 제공 로직을 사용하여 웹 사이트, 휴대폰, 연결된 TV, 태블릿, OTT 디바이스, 셋톱 박스 및 게임 콘솔 등 여러 미디어 플랫폼을 정확하게 측정할 수 있습니다. 다운로드한 콘텐츠도 측정할 수 있습니다. 사용자 시청 참여에 대한 통찰력을 통해 시청자가 참여한 기간, 시간, 장소를 파악할 수 있습니다. Media SDK는 추적을 위해 **Media Collection API**&#x200B;를 사용합니다. 애플리케이션에 사용자 정의 추적 기능이 필요한 경우 Media Collection API를 사용자 정의할 수 있습니다. Media SDK에서 지원하지 않는 디바이스의 경우 Media Collection API를 사용할 수 있습니다.

스트리밍 미디어용 Adobe Analytics 솔루션은 다음 미디어 플랫폼용으로 제공됩니다.

* 웹
* 모바일
* OTT
* 스트리밍 미디어 또는 서버 간 통합에 사용할 수 있는 연결된 디바이스

자세한 내용은 [지원되는 디바이스 및 플랫폼](#_Supported_devices_and)을 참조하십시오.

>[!IMPORTANT]
>
>스트리밍 미디어용 Adobe Analytics를 구현하려면 Adobe 영업 담당자 또는 계정 관리자에게 문의하여 스트리밍 미디어가 제품 포트폴리오에 포함되어 있는지 확인하십시오.

## 스트리밍 미디어용 Media SDK {#media-sdks}

스트리밍 미디어용 Media SDK는 JavaScript, Android, iOS, tvOS, Chromecast 및 Roku 플랫폼에서 사용할 수 있습니다.

Media SDK 다운로드 및 설치에 대한 자세한 내용은 [Media SDK, 태그를 사용한 확장 기능 및 OTT SDK 가져오기](/help/getting-started/download-sdks.md)를 참조하십시오.


## Media Collection API {#media-collection-apis}

**Media Collection API**&#x200B;는 미디어 분석 구현을 사용자 정의할 수 있게 합니다. SDK 등을 사용하여 작업을 수행하려면 Media Collection API를 사용해 Adobe 서버를 직접 호출하십시오. 데이터 수집을 사용자 정의하여 스트리밍 미디어 데이터에 대해 탐색하고 통찰력을 얻거나 중요한 질문에 답변이 되는 보고서를 생성하십시오.

Media Collection API 사용에 대한 자세한 내용은 [Steaming Media API 설명서](/help/implementation/media-collection-api/mc-api-overview.md)를 참조하십시오.

## Adobe 확장 기능 {#adobe-extensions}

* [**오디오 및 비디오 확장 기능용 Adobe Media Analytics**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=ko)(Media Analytics 확장 기능)은 iOS 및 tvOS 구현에 필요합니다. 태그 사이트 또는 프로젝트에 추적기 인스턴스를 추가하는 기능을 제공합니다. MA 확장 기능에는 Analytics 확장 기능 및 Experience Cloud ID 확장 기능도 필요합니다.

* [Analytics 확장 기능 v1.6 이상](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=ko-KR)—이 확장 기능을 사용하면 Adobe Experience Platform Web SDK JavaScript 라이브러리를 로드하여 데이터를 Adobe 솔루션으로 보낼 수 있습니다.

* [Experience Cloud ID 확장 기능](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=ko-KR)—이 확장 기능은 모든 Experience Cloud 솔루션에서 방문자를 식별하는 Experience Cloud ID 서비스를 구현합니다. Experience Cloud ID 서비스는 Adobe Experience Platform의 개인화 확장 기능입니다.