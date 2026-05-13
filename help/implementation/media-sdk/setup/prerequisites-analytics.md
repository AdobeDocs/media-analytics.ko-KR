---
title: Adobe Analytics 전용 구현을 위한 사전 요구 사항
description: Adobe Analytics 전용 구현을 위한 스트리밍 미디어용 Adobe Analytics 추가 기능을 사용하기 위한 사전 요구 사항에 대해 알아봅니다
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
TQID: https://experienceleague.adobe.com/falbDtUtqAMtmtQs2jLpEvUKmwvATotVu8njuTNZ09k
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 243
ht-degree: 14%

---

# Adobe Analytics 전용 구현을 위한 사전 요구 사항

이 섹션에 설명된 전제 조건은 Adobe-Analytics 전용 구현을 위한 스트리밍 미디어용 Adobe Analytics 추가 기능 구현(Edge을 사용하지 않는 경우)에만 적용됩니다.

1. **일반 필수 구성 요소를 완료하십시오.**<br>
Adobe Analytics 전용 구현용 또는 Edge 구현용 Streaming Media 서비스를 구현하는지 여부에 관계없이 [일반 사전 요구 사항](/help/getting-started/prereqs.md)을 충족하는지 확인하십시오.

1. **Adobe Analytics 구현이 있는지 확인**<br>
Analytics 전용 구현을 위해 스트리밍 미디어용 Adobe Analytics 추가 기능을 구현하는 경우 Adobe Analytics 기본 구현도 필요합니다. 자세한 내용은 [Adobe Analytics 구현](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)을 참조하십시오.

1. **미디어 추적 서버 URL 가져오기**<br>
미디어 추적 서버 URL은 Adobe Analytics 담당자에게 문의하십시오. 모바일 SDK, JavaScript SDK 및 Roku용 비수집 API 추적 서버의 `collection-api-server` URL입니다. API 구현을 위한 도메인 이름은 다음과 같습니다. `[your_namespace].hb-api.omtrdc.net`.

1. **현재 Media SDK을 다운로드하거나 필요한 확장을 구현합니다.**<br>
구현 경로에 따라 웹, 모바일 또는 OTT 플랫폼용 [현재 SDK을 다운로드](/help/getting-started/download-sdks.md)합니다. 스트리밍 미디어용 Adobe Analytics 추가 기능을 활성화하려면 필수 확장 기능을 구현해야 합니다.

1. **Adobe Analytics 보고서 사용**<br>
Analytics에서 보고서를 활성화하고 수집 중인 콘텐츠 및 광고 데이터를 보려면 Analytics에서 보고서를 활성화해야 합니다. [미디어 보고서 지원](/help/reporting/media-reports-enable.md)을 확인하십시오.
