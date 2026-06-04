---
title: 태그를 사용하는 스트리밍 미디어용 Android 설정
description: Adobe 태그 확장을 사용하여 Android에 대한 스트리밍 미디어 컬렉션을 구성합니다. Edge Network용 스트리밍 미디어 태그 확장.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 태그를 사용하는 스트리밍 미디어용 Android 설정

데이터 수집 UI에서 관리되는 미디어 설정으로 Android 모바일 속성을 통해 Tags 앱에 대한 스트리밍 미디어 컬렉션을 구성할 수 있습니다. 이 페이지에서는 태그 구성에 대해 설명합니다. 대신 코드에서 SDK을 구성하려면 [스트리밍 미디어용 Android 설정](android.md)을 참조하십시오.

* **필수 구성 요소**:
   * [Edge 구현 개요](overview.md)([!UICONTROL Media Analytics]이(가) 활성화된 스키마, 데이터 세트, 데이터 스트림)를 완료합니다.
   * 데이터 수집 UI에서 모바일 속성을 만듭니다. [Edge Network용 Adobe 스트리밍 미디어](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)를 참조하십시오.

## 확장 구성

1. 데이터 수집 UI에서 모바일 속성을 열고 **[!UICONTROL 확장]**&#x200B;을 선택합니다.
1. **[!UICONTROL 카탈로그]** 탭에서 **Edge Network용 Adobe 스트리밍 미디어** 확장을 찾아 **[!UICONTROL 설치]**&#x200B;를 선택합니다.
1. 다음을 설정한 다음 저장합니다.
   * **[!UICONTROL 채널]**: 각 세션에서 보고된 채널 이름입니다.
   * **[!UICONTROL 플레이어 이름]**: 사용 중인 미디어 플레이어의 이름입니다.
   * **[!UICONTROL 응용 프로그램 버전]**: 플레이어 응용 프로그램의 버전입니다.
1. 변경 사항을 게시한 다음 `Core`, `Edge`, `EdgeIdentity` 및 `EdgeMedia` 종속성을 앱에 추가하고 Mobile Core에 등록합니다.

## 미디어 이벤트 추적

속성이 게시되고 추적기가 만들어진 상태에서 추적기 메서드를 사용하여 각 미디어 이벤트를 추적합니다. 정확한 호출은 각 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md) 페이지에서 **Android** 탭을 참조하십시오.

## 다음 단계

구현이 완료되면 [Edge 구현에 대한 보고를 설정](/help/reporting/setup/edge-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [Edge Network용 Adobe 스트리밍 미디어](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [스트리밍 미디어용 Android 설정(코드)](android.md)
>* [이벤트 개요](/help/implementation/events/overview.md)
