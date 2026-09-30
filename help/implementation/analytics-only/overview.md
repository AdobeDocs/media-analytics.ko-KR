---
title: Analytics 전용 구현 개요
description: Analytics 전용 구현에 사용되는 스트리밍 미디어용 Adobe Analytics 추가 기능에 대한 사전 요구 사항 및 구현 방법입니다.
feature: Streaming Media
role: User, Admin, Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 5%
---
# Analytics 전용 구현 개요

Analytics 전용 구현은 스트리밍 미디어용 Adobe Analytics 추가 기능을 사용하여 Edge Network 없이 Adobe Analytics으로 직접 데이터를 전송합니다. 이러한 메서드는 계속 완벽하게 지원됩니다. 새로운 구현의 경우 Adobe은 Adobe Analytics 외에도 Customer Journey Analytics, Adobe Journey Optimizer 및 Real-Time CDP에서 데이터를 사용할 수 있도록 하므로 대신 [Edge 구현](/help/implementation/edge/overview.md)을 권장합니다.

## 사전 요구 사항

1. **일반 필수 구성 요소를 완료합니다.** [일반 필수 구성 요소](/help/getting-started/prereqs.md)를 참조하세요.

1. **Adobe Analytics 구현을 확인하십시오.** Analytics 전용 스트리밍 미디어 구현에는 기본 Adobe Analytics 구현이 필요합니다. [Adobe Analytics 구현](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ko)을 참조하세요.

1. **미디어 추적 서버 URL을 가져옵니다.** 미디어 추적 서버 URL(`collection-api-server` URL)은 Adobe Analytics 담당자에게 문의하십시오. 도메인은 일반적으로 `[your_namespace].hb-api.omtrdc.net` 패턴을 따릅니다.

1. **SDK을 다운로드하거나 확장을 설치하십시오.** 플랫폼에 따라 [현재 SDK을 다운로드](/help/getting-started/download-sdks.md)하거나 필요한 태그 확장을 설치하십시오.

## 구현 방법 선택

각 페이지에서는 스트리밍 미디어별 설정을 다룹니다. 이벤트별 및 변수별 코드는 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md)에 있습니다.

| 코드베이스 | 코드 내 | 태그 사용 |
|---|---|---|
| 웹(JavaScript) | [JavaScript](javascript.md) | [Media Analytics 태그 확장](javascript-tags.md) |
| Chromecast | [Chromecast](chromecast.md) | — |
| Roku | [Roku 2.x](roku-2x.md) | — |
| API | [미디어 컬렉션 API](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/implementation) | — |

## 다음 단계

구현이 완료되면 [Analytics 전용 구현에 대한 보고를 설정](/help/reporting/setup/analytics-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [구현 개요](/help/implementation/overview.md)
>* [이벤트 개요](/help/implementation/events/overview.md)
>* [변수 개요](/help/implementation/variables/overview.md)
