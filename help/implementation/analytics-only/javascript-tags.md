---
title: Media Analytics 태그 확장 설정
description: Adobe Media Analytics(3.x SDK) for Audio and Video 태그 확장 을 사용하여 Analytics 전용 스트리밍 미디어를 구현합니다.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 12%

---

# Media Analytics 태그 확장 설정

오디오 및 비디오 태그 확장 용 Adobe Media Analytics(3.x SDK)는 수동으로 JavaScript을 설치하지 않고 태그를 통해 JavaScript(3.x)용 Media SDK을 배포합니다. 이 페이지에서는 태그 구성에 대해 설명합니다. 대신 코드에 SDK을 설치하려면 [스트리밍 미디어용 JavaScript 설정](javascript.md)을 참조하십시오. 새로운 구현의 경우 권장되는 [웹 SDK 태그 확장](/help/implementation/edge/web-sdk-tags.md) Edge 경로를 고려하십시오.

* **필수 구성 요소**: [Analytics 전용 구현 개요](overview.md)를 완료합니다.

## 확장 설치 및 구성

데이터 수집 UI에서 확장을 설치 및 구성하여 태그 사용 사이트에 미디어 추적기 인스턴스를 추가합니다. 설치 및 구성에 대한 자세한 내용은 [Adobe Media Analytics(3.x SDK) for Audio and Video 확장](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=ko)을 참조하십시오.

## 미디어 이벤트 추적

확장이 구성된 상태에서 추적기 메서드를 사용하여 각 미디어 이벤트를 추적합니다. 정확한 호출은 각 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md) 페이지에서 **Media SDK JS 3.x** 탭을 참조하십시오.

## 다음 단계

구현이 완료되면 [Analytics 전용 구현에 대한 보고를 설정](/help/reporting/setup/analytics-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [오디오 및 비디오 확장 기능용 Adobe Media Analytics(3.x SDK)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=ko)
>* [스트리밍 미디어용 JavaScript 설정(코드)](javascript.md)
>* [이벤트 개요](/help/implementation/events/overview.md)
