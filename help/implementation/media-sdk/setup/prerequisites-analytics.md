---
title: Adobe Analytics 전용 구현을 위한 사전 요구 사항
description: Adobe Analytics 전용 구현을 위한 스트리밍 미디어용 Adobe Analytics 추가 기능을 사용하기 위한 사전 요구 사항에 대해 알아봅니다
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 43%

---

# Adobe Analytics 전용 구현을 위한 사전 요구 사항

이 섹션에 설명된 전제 조건은 Adobe-Analytics 전용 구현을 위한 스트리밍 미디어용 Adobe Analytics 추가 기능 구현(Edge을 사용하지 않는 경우)에만 적용됩니다.

1. **일반 필수 구성 요소를 완료합니다**<br>
Adobe Analytics 전용 구현용 또는 Edge 구현용 Streaming Media 서비스를 구현하는지 여부에 관계없이 [일반 사전 요구 사항](/help/getting-started/prereqs.md)을 충족하는지 확인하십시오.

1. **Adobe Analytics 구현이 있는지 확인**<br>
Analytics 전용 구현을 위해 스트리밍 미디어용 Adobe Analytics 추가 기능을 구현하는 경우 Adobe Analytics 기본 구현도 필요합니다. 자세한 내용은 [Adobe Analytics 구현](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ko)을 참조하십시오.

1. **미디어 추적 서버 URL 얻기**<br>
미디어 추적 서버 URL은 Adobe Analytics 담당자에게 문의하십시오. 모바일 SDK, JavaScript SDK 및 Roku용 비수집 API 추적 서버의 `collection-api-server` URL입니다. API 구현을 위한 도메인 이름은 다음과 같습니다. `[your_namespace].hb-api.omtrdc.net`.

1. **현재 Media SDK 다운로드 또는 필요한 확장 기능 구현**<br>
구현 경로에 따라 웹, 모바일 또는 OTT 플랫폼용 [현재 SDK를 다운로드](/help/getting-started/download-sdks.md)하십시오. 스트리밍 미디어용 Adobe Analytics 추가 기능을 활성화하려면 필수 확장 기능을 구현해야 합니다.

1. **Adobe Analytics 보고서 활성화**<br>
Analytics에서 보고서를 활성화하고 수집 중인 콘텐츠 및 광고 데이터를 보려면 Analytics에서 보고서를 활성화해야 합니다. [미디어 보고서 지원](/help/reporting/media-reports-enable.md)을 확인하십시오.
