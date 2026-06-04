---
title: 스트리밍 미디어용 웹 SDK 태그 확장 설정
description: Adobe Experience Platform Web SDK 태그 확장 기능에서 스트리밍 미디어 컬렉션을 구성합니다.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 스트리밍 미디어용 웹 SDK 태그 확장 설정

Adobe Experience Platform Web SDK 태그 확장을 사용하면 `alloy.js` 구성 코드 없이 데이터 수집 UI에서 스트리밍 미디어 컬렉션을 구성할 수 있습니다. 이 페이지에서는 태그 구성에 대해 설명합니다. 대신 코드에서 웹 SDK을 구성하려면 [스트리밍 미디어용 웹 SDK 설정](web-sdk.md)을 참조하십시오.

* **필수 구성 요소**:
   * [Edge 구현 개요](overview.md)([!UICONTROL Media Analytics]이(가) 활성화된 스키마, 데이터 세트, 데이터 스트림)를 완료합니다.
   * 웹 SDK 태그 확장을 설치하고 구성합니다. [웹 SDK 태그 확장 개요](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)를 참조하세요.

## 확장에서 스트리밍 미디어 구성

1. 데이터 수집 UI에서 웹 속성을 열고 **[!UICONTROL 확장]**&#x200B;을 선택합니다.
1. 설치된 **Adobe Experience Platform Web SDK** 확장에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다.
1. **[!UICONTROL 스트리밍 미디어]** 섹션을 확장하고 다음을 설정합니다.
   * **[!UICONTROL 채널]** — 각 세션에서 보고된 채널 이름.
   * **[!UICONTROL 플레이어 이름]** — 사용 중인 미디어 플레이어의 이름입니다.
   * **[!UICONTROL 응용 프로그램 버전]** — 플레이어 응용 프로그램의 버전입니다.
   * **[!UICONTROL 기본 ping 간격]** 및 **[!UICONTROL 광고 ping 간격]** — 기본 컨텐츠 및 광고의 ping 케이던스(초)입니다.
1. 확장 구성을 저장하고 변경 사항을 게시합니다.

## 미디어 이벤트 추적

확장을 구성한 상태에서 **[!UICONTROL 이벤트 보내기]** 작업(또는 `sendEvent` 명령)을 사용하여 각 미디어 이벤트를 보냅니다. 정확한 페이로드는 각 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md) 페이지에서 **웹 SDK** 탭을 참조하십시오.

## 다음 단계

구현이 완료되면 [Edge 구현에 대한 보고를 설정](/help/reporting/setup/edge-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [웹 SDK 태그 확장 개요](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)
>* [스트리밍 미디어용 웹 SDK 설정(코드)](web-sdk.md)
>* [이벤트 개요](/help/implementation/events/overview.md)
