---
title: 시작하기
description: 스트리밍 미디어용 Adobe Analytics을 시작합니다.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 6%

---


# 시작하기 {#getting-started}

Adobe Analytics for Streaming Media는 Media SDK와 Media Collection API의 두 가지 기본 구현 방법을 제공합니다.

![메서드](assets/getting-started2.png)

의 기본 제공 논리 사용 **Media SDK**, 웹 사이트, 휴대폰, 연결된 TV, 태블릿, OTT 장치, 셋톱 박스 및 게임 콘솔을 포함하여 여러 미디어 플랫폼을 정확하게 측정할 수 있습니다. 다운로드한 컨텐츠도 측정할 수 있습니다. 사용자가 참여하는 데 심도 있는 인사이트를 얻을 수 있으므로 뷰어가 참여하는 시간, 시기 및 위치를 파악할 수 있습니다. Media SDK는 **Media Collection API** 추적에 사용됩니다. 애플리케이션에 사용자 지정 추적 기능이 필요한 경우 Media Collection API를 사용자 지정할 수 있습니다. Media SDK에서 지원하지 않는 장치의 경우 Media Collection API를 사용할 수 있습니다.

Adobe Analytics 스트리밍 미디어 솔루션은 다음 미디어 플랫폼에 제공됩니다.

* 웹
* 모바일
* 위
* 스트리밍 미디어 또는 서버 간 통합에 사용할 수 있는 연결된 모든 장치

자세한 내용은 [지원되는 장치 및 플랫폼](#_Supported_devices_and).

>[!IMPORTANT]
>
>Adobe Analytics 스트리밍 미디어를 구현하려면 Adobe 영업 담당자 또는 계정 관리자에게 문의하여 스트리밍 미디어가 제품 포트폴리오에 포함되어 있는지 확인하십시오.

## 스트리밍 미디어용 Media SDK {#media-sdks}

스트리밍 미디어용 Media SDK는 JavaScript, Android, iOS, tvOS, Chromecast 및 Roku 플랫폼에서 사용할 수 있습니다.

Media SDK 다운로드 및 설치에 대한 자세한 내용은 [Media SDK, 태그를 사용한 확장 프로그램 및 OTT SDK를 가져옵니다](/help/getting-started/download-sdks.md).


## Media Collection API {#media-collection-apis}

다음 **Media Collection API** media analytics 구현을 사용자 지정할 수 있습니다. Media Collection API를 사용하여 Adobe의 서버를 직접 호출하여 SDK 등을 사용하여 수행할 수 있는 거의 모든 작업을 수행할 수 있습니다. 데이터 컬렉션을 사용자 지정하여 스트리밍 미디어 데이터에 대한 중요한 질문에 답하거나, 통찰력을 얻을 수 있는 보고서를 만들 수 있습니다.

Media Collection API 사용에 대한 자세한 내용은 [스트리밍 미디어 API 설명서](/help/implementation/media-collection-api/mc-api-overview.md).

## Adobe 확장 {#adobe-extensions}

>[!NOTE]
>
>확장에 대한 소개 필요

* 다음 [**Adobe Medium Analytics for Audio 및 Video 확장**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) (Media Analytics 확장)은 iOS 및 tvOS 구현에 필요합니다. 태그 사이트 또는 프로젝트에 추적기 인스턴스를 추가하는 기능을 제공합니다. MA 확장 프로그램에는 Analytics 확장 및 Experience Cloud ID 확장 프로그램이 필요합니다.

* [Analytics 확장 v1.6 이상](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en)—이 확장을 사용하면 Adobe Experience Platform Web SDK Javascript 라이브러리를 로드하여 데이터를 Adobe 솔루션으로 보낼 수 있습니다.

* [Experience Cloud ID 확장](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)—이 확장은 모든 Experience Cloud 솔루션에서 방문자를 식별하는 Experience Cloud ID 서비스를 구현합니다. Experience Cloud ID 서비스는 Adobe Experience Platform의 개인화 확장입니다.
