---
title: Adobe Analytics 전용 구현을 위한 사전 요구 사항
description: Adobe Analytics 전용 구현에 스트리밍 미디어를 사용하기 위한 사전 요구 사항에 대해 알아봅니다
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: c4d058ee82f4995f42bfe21c0442004f1f7ea4af
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 58%

---

# Adobe Analytics 전용 구현을 위한 사전 요구 사항

이 섹션에 설명된 전제 조건은 Adobe 분석 전용 구현으로 Streaming Media를 구현하는 것(Edge를 사용하지 않는 경우)에만 적용됩니다.

1. **일반 사전 요구 사항 완료**<br>
Adobe Analytics 전용 구현용 Streaming Media를 구현하든 Edge 구현용 Streaming Media를 구현하든 다음을 충족하는지 확인합니다. [일반 사전 요구 사항](/help/getting-started/prereqs.md).

1. **Adobe Analytics 구현이 있는지 확인합니다**<br>
Analytics 전용 구현으로 스트리밍 미디어를 구현하는 경우 Adobe Analytics 기본 구현도 필요합니다. 자세한 내용은 [Adobe Analytics 구현](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)을 참조하십시오.

1. **미디어 추적 서버 URL 얻기**<br>
미디어 추적 서버 URL은 Adobe Analytics 담당자에게 문의하십시오. 이는 `collection-api-server` 모바일 SDK, JavaScript SDK 및 Roku용 비수집 API 추적 서버의 URL입니다. API 구현을 위한 도메인 이름은 다음과 같습니다. `[your_namespace].hb-api.omtrdc.net`.

1. **현재 Media SDK 다운로드 또는 필요한 확장 기능 구현**<br>
구현 경로에 따라 웹, 모바일 또는 OTT 플랫폼용 [현재 SDK를 다운로드](/help/getting-started/download-sdks.md)하십시오. 스트리밍 미디어용 Adobe Analytics 확장 경로를 활성화하려면 필수 확장 기능을 구현해야 합니다.

1. **Adobe Analytics 보고서 활성화**<br>
Analytics에서 보고서를 활성화하고 수집 중인 콘텐츠 및 광고 데이터를 보려면 Analytics에서 보고서를 활성화해야 합니다. [미디어 보고서 지원](/help/reporting/media-reports-enable.md)을 확인하십시오.
