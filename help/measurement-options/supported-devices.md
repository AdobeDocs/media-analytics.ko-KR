---
title: 지원되는 디바이스 및 플랫폼
description: 오디오 및 비디오용 Adobe Analytics를 사용하면 모든 디바이스에서 각 미디어 스트림을 수집하고 보고할 수 있습니다.
translation-type: tm+mt
source-git-commit: a8fec1747e688473af7a5eabbc4f9968772b5db3
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 15%

---


# 지원되는 디바이스 및 플랫폼 {#devices-supported}

>[!IMPORTANT]
>
>2021년 8월 31일에 버전 4 Mobile SDK에 대한 지원이 종료됨에 따라 Adobe는 iOS 및 Android용 Media Analytics SDK에 대한 지원도 종료할 예정입니다.  자세한 내용은 [Media Analytics SDK 지원 종료 FAQ를 참조하십시오](/help/sdk-implement/end-of-support-faqs.md).

오디오 및 비디오용 Adobe Analytics는 다음을 비롯한 모든 주요 장치를 지원합니다.

* iOS 및 Android 스마트폰 및 태블릿
* ROKU, AppleTV, FireTV 및 Android TV용 OTT 장치
* 데스크탑 및 랩탑용 JavaScript 브라우저

미디어 SDK는 새로운 버전의 디바이스가 출시되면 정기적으로 업데이트되며 SDK를 사용하여 Brightcove 및 Oyala를 비롯한 오늘날 가장 큰 미디어 플레이어와 통합할 수 있습니다.

현재 SDK 지원이 없는 디바이스 또는 플랫폼이나 SDK를 사용하지 않으려는 경우 Media Collection API를 구현할 수 있습니다. Media Collection API를 사용하면 디바이스 또는 플랫폼에서 Media Analytics 백엔드로 바로 RESTful API 호출을 만들 수 있습니다.

아래 표에는 현재 지원되는 디바이스 및 플랫폼이 나와 있습니다. 최신 버전의 SDK를 다운로드하려면 [SDK 다운로드를 참조하십시오](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html). 장치가 목록에 없으면 고객 지원 센터 또는 솔루션 컨설턴트에게 해당 장치의 상태를 문의하십시오.

| 스트리밍 플랫폼 및 디바이스 |  | AEP SDK를 통한 미디어 실행 확장 | Media SDK | Media Collection API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| 웹/모바일 웹 |  |  |  |  |
|  | JavaScript 브라우저 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| 모바일 앱 |  |  |  |  |
|  | iOS 장치 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android 장치 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windows 장치 |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV(tvOS) | 2020년 예정 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>(기본) |
|  | Fire TV(Fire OS) | 2020년 예정 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | 2020년 예정 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | 게임 콘솔(예: Xbox ONE, Sony PS3/PS4) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | 상위 박스 설정(예: Exfinity X1) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | 스마트 TV(예: 삼성, LG, 소니, 비지오) |  | ![](/help/assets/icon-blue-check.png)   <br>(웹 기반)    | ![](/help/assets/icon-blue-check.png) |
| 기타 |  |  |  |  |
|  | 새로운 연결된 디바이스 |  |  | ![](/help/assets/icon-blue-check.png) |

1. 이러한 SDK에 대한 지원은 2021년 8월 31일에 종료됩니다. 자세한 내용은 [Media Analytics SDK 지원 종료 FAQ를 참조하십시오](/help/sdk-implement/end-of-support-faqs.md).

각 SDK에 대해 지원되는 최소 플랫폼 버전에 대한 자세한 내용은 [최소 플랫폼 버전 지원을 참조하십시오.](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/setup/setup-overview.html)
