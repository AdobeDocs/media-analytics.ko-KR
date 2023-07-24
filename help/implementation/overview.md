---
title: Adobe Analytics 또는 Customer Journey Analytics용 Streaming Media 구현
description: Streaming Media 구현 경로에 대해 자세히 알아봅니다.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 984f058fda15b1c5e960e4c8d8e2378308d2b541
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 11%

---

# Adobe Analytics용 Streaming Media 구현 또는 Customer Journey Analytics

스트리밍 미디어를 구현하는 방법에는 여러 가지가 있습니다. 이 페이지에 설명된 구현 방법에 대해 지원되는 장치 및 플랫폼에 대한 자세한 비교는 다음을 참조하십시오. [지원되는 디바이스 및 플랫폼](/help/getting-started/supported-devices.md).

## Edge 구현 방법

모든 신규 Adobe Analytics 또는 Customer Journey Analytics 고객을 위해 Media Analytics를 구현할 때 Edge를 사용하는 것이 좋습니다.

* **Edge Network SDK / 확장 프로그램용 미디어:** iOS 및 Android 장치에서 데이터를 수집하여 Edge로 전송합니다. 그런 다음 데이터를 Customer Journey Analytics 또는 Adobe Analytics으로 전송할 수 있습니다.

  Edge Network SDK/확장용 Media에 대한 자세한 내용은 다음을 참조하십시오. [Experience Platform Edge로 Media Analytics 설치](/help/implementation/edge/implementation-edge.md).

  >[!NOTE]
  >
  >이 구현 방법은 현재 Web SDK 또는 Roku를 지원하지 않습니다. 그러나 Media Edge API로 구현할 때는 둘 다 지원됩니다.

* **Media Edge API:** 모든 장치 또는 형식(모바일, 웹 및 OTT 장치 포함)에서 데이터를 수집하도록 사용자 정의하고 Edge로 데이터를 전송할 수 있습니다. 그런 다음 데이터를 Customer Journey Analytics 또는 Adobe Analytics으로 전송할 수 있습니다.

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![CJA 워크플로](assets/cja-implementation.png)

## Adobe Analytics 전용 구현 메서드

위에서 설명한 Edge 구현 방법은 Customer Journey Analytics 및 Adobe Analytics 모두에 대해 권장되며, 특히 새 구현에 대해 권장됩니다.

Edge 구현 방법 외에도 다른 구현 방법을 사용할 수 있습니다. 이러한 구현 방법은 Adobe Analytics에서 사용하도록 설계되었습니다. 그러나 다음 구현 방법을 사용하는 기존 고객은 여전히 다음을 만들어 Customer Journey Analytics에서 데이터를 사용할 수 있습니다. [Analytics 소스 연결](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html).

* **태그 포함 미디어 확장:** 오디오 및 비디오용 Adobe Medium Analytics 확장은 태그가 활성화된 사이트 또는 프로젝트에 미디어 추적기 인스턴스를 추가하는 기능을 제공합니다. 데이터가 Adobe Analytics으로 전송됩니다.

  태그를 사용한 Media Extension 설치, 구성 및 구현에 대한 자세한 내용은 다음을 참조하십시오. [오디오 및 비디오 확장 기능용 Adobe Medium Analytics(3.x SDK) 개요](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **Media SDK:**  Media SDK를 사용하면 웹 사이트, 휴대폰, 연결된 TV, 태블릿, OTT 장치, 셋톱 박스 및 게임 콘솔 등 여러 미디어 플랫폼을 측정할 수 있습니다. (자세한 내용은 [지원되는 디바이스 및 플랫폼](/help/getting-started/supported-devices.md).)

  Media SDK는 추적을 위해 Media Collection API를 사용합니다. 데이터가 Adobe Analytics으로 전송됩니다.

  Media SDK 및 확장 기능 다운로드 및 설치에 대한 자세한 내용은 [Media SDK, 태그를 사용한 확장 기능 및 OTT SDK 가져오기](/help/getting-started/download-sdks.md)를 참조하십시오.

* **Media Collection API:** Media Collection API는 사용자 지정할 수 있으므로 사용자 지정 추적 기능이 필요한 애플리케이션 및 Media SDK에서 지원하지 않는 디바이스에 사용할 수 있습니다. Media Collection API는 RESTful HTTP 호출을 사용하여 오디오 및 비디오 이벤트를 추적합니다. 데이터가 Adobe Analytics으로 전송됩니다.

  Media Collection API 사용에 대한 자세한 내용은 [Media Collection API](media-collection-api/mc-api-overview.md)를 참조하십시오.


![Analytics 워크플로](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
