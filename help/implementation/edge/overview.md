---
title: Edge 구현 개요
description: Edge Network을 통해 스트리밍 미디어 데이터를 수집하는 데 필요한 Adobe Experience Platform 스키마, 데이터 세트 및 데이터 스트림을 설정합니다.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 5%

---

# Edge 구현 개요

Adobe Experience Platform Edge Network을 사용하면 여러 제품을 대상으로 한 데이터를 단일 엔드포인트로 보낸 다음, 적절한 정보를 각 제품에 전달할 수 있습니다. 이를 통해 여러 데이터 솔루션에 대한 구현 노력을 통합하고 Adobe Analytics 및 Customer Journey Analytics 모두에 대한 스트리밍 미디어 컬렉션을 구현하는 권장 방법입니다.

웹 SDK, 모바일 SDK(iOS 또는 Android), Roku SDK 또는 Media Edge API 등 사용하는 코드 베이스에 관계없이 먼저 스키마 만들기, 데이터 세트 만들기, 데이터 스트림 구성 등 이 페이지에 설명된 플랫폼 설정을 완료해야 합니다.

## 사전 요구 사항

1. **일반 필수 구성 요소를 완료합니다.** [일반 필수 구성 요소](/help/getting-started/prereqs.md)를 참조하세요.

1. **호환 가능한 Adobe 솔루션을 확인합니다.** 작동하는 Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer 또는 Real-Time Customer Data Platform 구현이 있어야 합니다.
   * [Customer Journey Analytics 안내서](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=ko)
   * [Adobe Analytics 구현](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
   * [Adobe Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ko)
   * [Real-Time Customer Data Platform 설명서](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

## Adobe Experience Platform에서 스키마 설정

Adobe은 Adobe Experience Platform을 사용하는 애플리케이션 간에 데이터 수집을 표준화하기 위해 공개적으로 문서화된 개방형 XDM(Experience Data Model) 표준을 만들었습니다.

1. [UI에서 스키마 만들기 및 편집](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)에 설명된 대로 Adobe Experience Platform에서 스키마 만들기를 시작합니다.

1. 스키마 세부 정보 페이지에서 **[!UICONTROL 경험 이벤트]**&#x200B;를 스키마의 기본 클래스로 선택합니다.

   ![추가된 필드 그룹](assets/schema-experience-event.png)

1. **[!UICONTROL 다음]**&#x200B;을 선택합니다.

1. 스키마 표시 이름과 설명을 지정한 다음 **[!UICONTROL 마침]**&#x200B;을 선택합니다.

1. **[!UICONTROL 컴포지션]** 영역의 **[!UICONTROL 필드 그룹]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 선택한 다음 다음 다음 필드 그룹을 검색하여 스키마에 추가하십시오.
   * `End User ID Details`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   필드 그룹을 추가하면 **[!UICONTROL 필드 그룹]** 섹션에 표시됩니다.

   ![추가된 필드 그룹](assets/schema-field-groups-added.png)

1. 변경 내용을 저장하려면 **[!UICONTROL 저장]**&#x200B;을 선택하세요.

1. (선택 사항) Media Edge API에서 사용되지 않는 특정 필드를 숨길 수 있습니다. 이러한 필드를 숨기면 스키마를 읽기 쉬워지지만 필수는 아닙니다. 이 필드는 `MediaAnalytics Interaction Details` 필드 그룹의 필드만 참조합니다.

   +++ 를 확장하여 숨길 수 있는 필드에 대한 지침을 봅니다.

   1. **[!UICONTROL 구조]** 영역에서 `Media Collection Details` 필드를 선택한 다음 **[!UICONTROL 관련 필드 관리]**&#x200B;를 선택합니다.

      ![관련 필드 관리](assets/manage-related-fields.png)

   1. **[!UICONTROL 필드에 대한 표시 이름을 표시]**&#x200B;하는 옵션을 활성화한 다음 다음과 같이 스키마를 업데이트합니다.

      * `Media Collection Details` > `Advertising Details` 필드에서 보고 필드 `Ad Completed`, `Ad Started` 및 `Ad Time Played`을(를) 숨깁니다.

      * `Media Collection Details` > `Advertising Pod Details` 필드에서 다음 보고 필드를 숨깁니다. `Ad Break ID`

      * `Media Collection Details` > `Chapter Details` 필드에서 보고 필드 `Chapter Completed`, `Chapter ID`, `Chapter Started` 및 `Chapter Time Played`을(를) 숨깁니다.

      * `Media Collection Details` 필드에서 `List Of States` 필드를 숨깁니다.

        ![미디어 컬렉션 상태 숨기기](assets/schema-hide-media-collection-states.png)

      * `Media Collection Details` > `List Of States End` 및 `Media Collection Details` > `List Of States Start` 필드에서 보고 필드 `Player State Count`, `Player State Set` 및 `Player State Time`을(를) 숨깁니다.

        ![숨길 필드](assets/schema-hide-listofstates.png)

      * `Media Collection Details` > `Qoe Data Details` 필드에서 보고 필드 `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Impacted Streams`, `Buffer Events`, `Dropped Frame Impacted Streams`, `Drops Before Starts`, `Errors`, `External Error IDs`, `Error Impacted Streams`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Impacted Streams`, `Stalling Events`, `Total Buffer Duration` 및 `Total Stalling Duration`을(를) 숨깁니다.

      * `Media Collection Details` > `Session Details` 필드에서 보고 필드 `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Completes`, `Chapter Count`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Segment Views`, `Media Downloaded Flag`, `Media Starts`, `Media Session ID`, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pev3`, `Pccr`, `Total Pause Duration`, `Unique Time Played` 및 `Video Segment`을(를) 숨깁니다.

   1. 변경 내용을 저장하려면 **[!UICONTROL 확인]**&#x200B;을 선택하세요.

   1. **[!UICONTROL 구조]** 영역에서 **[!UICONTROL 필드에 대한 표시 이름을 표시]**&#x200B;하는 옵션을 활성화한 다음 `List Of Media Collection Downloaded Content Events` 필드를 선택합니다.

   1. **[!UICONTROL 관련 필드 관리]**&#x200B;를 선택한 후 다음과 같이 스키마를 업데이트합니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` 필드에서 보고 필드 `Ad Completed`, `Ad Started` 및 `Ad Time Played`을(를) 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` 필드에서 다음 보고 필드를 숨깁니다. `Ad Break ID`

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` 필드에서 보고 필드 `Chapter Completed`, `Chapter ID`, `Chapter Started` 및 `Chapter Time Played`을(를) 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` 필드에서 `List Of States` 필드를 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` 및 `Media Collection Details` > `List Of States Start` 필드에서 보고 필드 `Player State Count`, `Player State Set` 및 `Player State Time`을(를) 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` 필드에서 보고 필드 `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Events`, `Buffer Impacted Streams`, `Drops Before Starts`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Errors`, `External Error IDs`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, `Stalling Impacted Streams`, `Total Buffer Duration` 및 `Total Stalling Duration`을(를) 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` 필드에서 보고 필드 `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Content Completes`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Media Segment Views`, `Media Session ID`, `Media Session Server Timeout`, `Media Starts`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pccr`, `Pev3`, `Total Pause Duration`, `Unique Time Played` 및 `Video Segment`을(를) 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` 필드에서 `Media Session ID` 필드를 숨깁니다.

   1. 변경 내용을 저장하려면 **[!UICONTROL 확인]**&#x200B;을 선택하세요.

   1. **[!UICONTROL 구조]** 영역에서 `Media Reporting Details` 필드를 선택한 다음 **[!UICONTROL 관련 필드 관리]**&#x200B;를 선택합니다.

   1. **[!UICONTROL 필드에 대한 표시 이름을 표시]**&#x200B;하는 옵션을 활성화한 다음 다음과 같이 스키마를 업데이트합니다.

      * `Media Reporting Details` 필드에서 `Error Details`, `List Of States End`, `List of States Start` 및 `Media Session ID` 필드를 숨깁니다.

   1. 변경 내용을 저장하려면 **[!UICONTROL 확인]** > **[!UICONTROL 저장]**&#x200B;을 선택합니다.

   +++

1. (선택 사항) 사용자 지정 메타데이터를 스키마에 추가할 수 있습니다. 이를 통해 특정 요구 사항 또는 컨텍스트에 대한 추가 사용자 정의 메타데이터를 포함할 수 있습니다. Media Edge API를 사용한 사용자 지정 메타데이터에 대한 자세한 내용은 [사용자 지정 메타데이터 지원](custom-metadata.md)을 참조하십시오.

   +++ 를 확장하여 스키마에 사용자 지정 메타데이터 추가에 대한 지침을 봅니다.

   1. **[!UICONTROL 계정 정보]** > **[!UICONTROL 할당된 조직]** > [!UICONTROL _&#x200B;**조직 이름**&#x200B;_] > **[!UICONTROL 테넌트]**&#x200B;를 선택하여 조직의 테넌트 이름을 찾습니다.

      사용자 정의 필드는 이 경로를 통해 수신됩니다. (예: 테넌트 이름: _dcbl → myCustomField 경로: _dcbl.myCustomField.)

   1. 정의된 미디어 스키마에 사용자 정의 필드 그룹을 추가합니다.

      ![사용자 지정 메타데이터 추가](assets/add-custom-metadata-fieldgroup.png)

   1. 추적할 사용자 지정 필드를 필드 그룹에 추가합니다.

      ![사용자 지정 메타데이터 추가](assets/add-custom-fields.png)

   1. 요청 페이로드의 사용자 지정 필드에 대해 [생성된 경로](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/fields/overview#type-specific-properties)을(를) 사용합니다.

      ![사용자 지정 메타데이터 추가](assets/custom-fields-path.png)

   +++

1. [Adobe Experience Platform에서 데이터 세트 만들기](#create-a-dataset-in-adobe-experience-platform)를 계속합니다.

## Adobe Experience Platform에 데이터 세트 만들기

1. [Adobe Experience Platform에서 스키마 설정](#set-up-the-schema-in-adobe-experience-platform)에 설명된 대로 스키마를 설정해야 합니다.

1. [데이터 세트 UI 안내서](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=ko#create)에 설명된 대로 Adobe Experience Platform에서 데이터 세트 만들기를 시작합니다.

   데이터 세트에 대한 스키마를 선택할 때 이전에 만든 스키마를 선택합니다.

1. [Adobe Experience Platform에서 데이터 스트림 구성](#configure-a-datastream-in-adobe-experience-platform)을 계속합니다.

## Adobe Experience Platform에서 데이터 스트림 구성

1. [Adobe Experience Platform에서 데이터 세트 만들기](#create-a-dataset-in-adobe-experience-platform)에 설명된 대로 데이터 세트를 만들었는지 확인하십시오.

1. [데이터 스트림 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=ko)에 설명된 대로 새 데이터 스트림을 만듭니다.

   데이터 스트림을 생성할 때 다음을 선택합니다.

   * **[!UICONTROL 이벤트 스키마]** 필드에서 [Adobe Experience Platform에서 스키마를 설정](#set-up-the-schema-in-adobe-experience-platform)에서 만든 스키마를 선택합니다. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

     >[!IMPORTANT]
     >
     >**[!UICONTROL 매핑 저장 및 추가]**&#x200B;를 선택하지 마십시오. 이렇게 하면 타임스탬프 필드에 대한 매핑 오류가 발생합니다.

     ![데이터 스트림을 만들고 스키마 선택](assets/datastream-create-schema.png)

   * Adobe Analytics 또는 Customer Journey Analytics 사용 여부에 따라 다음 서비스 중 하나를 데이터스트림에 추가합니다.

      * **[!UICONTROL Adobe Analytics]**(Adobe Analytics을 사용하는 경우)

        Adobe Analytics을 사용하는 경우 [보고서 세트 만들기](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite)에 설명된 대로 보고서 세트를 정의합니다.

      * **[!UICONTROL Adobe Experience Platform]**(Customer Journey Analytics을 사용하는 경우)

     데이터스트림에 서비스를 추가하는 방법에 대한 자세한 내용은 [데이터스트림 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details)에서 &quot;데이터스트림에 서비스 추가&quot;를 참조하십시오.

     ![Adobe Analytics 서비스 추가](assets/datastream-add-service.png)

   * **[!UICONTROL 고급 옵션]**&#x200B;을 확장한 다음 **[!UICONTROL Media Analytics]** 옵션을 활성화합니다.

     ![Media Analytics 옵션](assets/datastream-media-check.png)

## 구현 방법 선택

스키마, 데이터 세트 및 데이터스트림을 적절히 사용하여 다음 코드베이스 중 하나를 구현하여 Edge Network으로 스트리밍 미디어 데이터 전송을 시작합니다. 각 페이지는 스트리밍 미디어별 설정을 다룹니다. 이벤트별 및 변수별 코드는 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md)에 있습니다.

| 코드베이스 | 코드 내 | 태그 사용 |
|---|---|---|
| 웹 | [웹 SDK](web-sdk.md) | [웹 SDK 태그 확장](web-sdk-tags.md) |
| iOS | [iOS](ios.md) | [iOS(태그)](ios-tags.md) |
| Android | [Android](android.md) | [Android(태그)](android-tags.md) |
| Roku | [Roku](roku.md) | — |
| API | [미디어 Edge API](media-edge-api.md) | — |

## 다음 단계

데이터 수집을 시작한 후 보고를 구성할 수 있습니다.

* [Edge 구현에 대한 보고 설정](/help/reporting/setup/edge-reporting.md)(Customer Journey Analytics)
* [Analytics 전용 구현에 대한 보고 설정](/help/reporting/setup/analytics-reporting.md)(데이터 스트림이 Adobe Analytics을 제공하는 경우)

>[!MORELIKETHIS]
>
>* [사용자 지정 메타데이터 지원](custom-metadata.md)
>* [XDM 보고 스키마](reporting-schema.md)
>* [이벤트 개요](/help/implementation/events/overview.md)
