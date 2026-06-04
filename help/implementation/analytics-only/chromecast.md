---
title: 스트리밍 미디어용 Chromecast 설정
description: Analytics 전용 스트리밍 미디어 구현을 위한 Chromecast용 Media SDK을 설치하고 구성합니다.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 10%

---

# 스트리밍 미디어용 Chromecast 설정

Chromecast용 Media SDK은 Chromecast 수신기 앱의 스트리밍 미디어 데이터를 Adobe Analytics으로 직접 전송합니다. SDK 및 해당 설명서는 GitHub에서 호스팅됩니다.

* **필수 구성 요소**:
   * [Analytics 전용 구현 개요](overview.md)를 완료합니다.
   * [Chromecast용 Media SDK을 다운로드합니다](/help/getting-started/download-sdks.md).

## SDK 설치 및 구성

표준 참조에 설명된 대로 SDK을 Chromecast 수신기 앱에 추가하고 추적기를 구성합니다.

* [Chromecast SDK 설정](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md)
* [Chromecast SDK API 참조](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)

## 미디어 이벤트 추적

추적기가 만들어진 상태에서 추적기 메서드를 사용하여 각 미디어 이벤트를 추적합니다. 정확한 호출은 각 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md) 페이지에서 **Chromecast** 탭을 참조하십시오.

## 다음 단계

구현이 완료되면 [Analytics 전용 구현에 대한 보고를 설정](/help/reporting/setup/analytics-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [Chromecast SDK API 참조](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)
>* [이벤트 개요](/help/implementation/events/overview.md)
>* [변수 개요](/help/implementation/variables/overview.md)
