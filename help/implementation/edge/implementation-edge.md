---
title: Edge Network을 사용하여 Adobe 스트리밍 미디어 서비스 구현
description: Experience Platform Edge을 사용하여 Adobe 스트리밍 미디어 서비스를 구현하는 방법에 대해 알아봅니다.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: dfdb1415-105e-4c41-bedc-ecb85ed1b1d9
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '2152'
ht-degree: 9%

---

# Edge Network을 사용하여 스트리밍 미디어 컬렉션 구현

Adobe Experience Platform Edge Network를 사용하면 여러 제품을 대상으로 한 데이터를 중앙 위치에 전송할 수 있습니다. Experience Edge는 적절한 정보를 원하는 제품에 전달합니다. 이 개념을 사용하면 특히 여러 데이터 솔루션에 걸쳐 구현 노력을 통합할 수 있습니다.

다음 그래픽은 Experience Platform Edge을 사용하여 Adobe Analytics 또는 Customer Journey Analytics에서 Analysis Workspace에서 데이터를 사용할 수 있도록 스트리밍 미디어 컬렉션 추가 기능을 구현하는 방법을 보여 줍니다.

![CJA 워크플로](assets/streaming-media-edge.png)

Experience Platform Edge을 사용하지 않는 구현 방법을 포함하여 모든 구현 옵션에 대한 개요를 보려면 [Adobe Analytics 또는 Customer Journey Analytics용 Streaming Media 서비스 구현](/help/implementation/overview.md)을 참조하십시오.

Adobe Experience Platform Web SDK, Adobe Experience Platform Mobile SDK, Adobe Experience Platform Roku SDK 또는 API를 사용하여 Experience Edge으로 스트리밍 미디어 컬렉션을 구현하는지 여부에 관계없이 먼저 다음 섹션을 완료해야 합니다.

## Adobe Experience Platform에서 스키마 설정

Adobe Experience Platform을 활용하는 애플리케이션 전체에서 사용할 데이터 수집을 표준화하기 위해, Adobe는 개방적이고 공개적으로 문서화된 표준인 XDM(경험 데이터 모델)을 만들었습니다.

스키마를 만들고 설정하려면:

1. [UI에서 스키마 만들기 및 편집](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)에 설명된 대로 Adobe Experience Platform에서 스키마 만들기를 시작합니다.

1. 스키마를 만들 때 스키마 세부 정보 페이지에서 스키마에 대한 기본 클래스를 선택할 때 [!UICONTROL **경험 이벤트**]&#x200B;를 선택합니다.

   ![추가된 필드 그룹](assets/schema-experience-event.png)

1. [!UICONTROL **다음**]&#x200B;을 선택합니다.

1. 스키마 표시 이름과 설명을 지정한 다음 [!UICONTROL **마침**]&#x200B;을 선택합니다.

1. [!UICONTROL **컴포지션**] 영역의 [!UICONTROL **필드 그룹**] 섹션에서 [!UICONTROL **추가**]&#x200B;를 선택한 다음 다음 다음 새 필드 그룹을 검색하여 스키마에 추가하십시오.
   * `End User ID Details`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   필드 그룹을 추가하면 다음과 같이 [!UICONTROL **필드 그룹**] 섹션에 표시됩니다.

   ![추가된 필드 그룹](assets/schema-field-groups-added.png)

1. 변경 내용을 저장하려면 [!UICONTROL **저장**]&#x200B;을 선택하세요.

1. (선택 사항) Media Edge API에서 사용되지 않는 특정 필드를 숨길 수 있습니다. 이러한 필드를 숨기면 스키마를 읽고 이해하는 것이 쉬워지지만 필수는 아닙니다. 이 필드는 `MediaAnalytics Interaction Details` 필드 그룹의 필드만 참조합니다.

   +++ 숨길 수 있는 필드에 대한 지침을 보려면 여기를 확장하십시오.

   1. [!UICONTROL **구조**] 영역에서 `Media Collection Details` 필드를 선택한 다음 [!UICONTROL **관련 필드 관리**]&#x200B;를 선택합니다.

      ![관련 필드 관리](assets/manage-related-fields.png)

   1. [!UICONTROL **필드에 대한 표시 이름을 표시**]&#x200B;하는 옵션을 활성화한 다음 다음과 같이 스키마를 업데이트합니다.

      * `Media Collection Details` > `Advertising Details` 필드에서 보고 필드 `Ad Completed`, `Ad Started` 및 `Ad Time Played`을(를) 숨깁니다.

      * `Media Collection Details` > `Advertising Pod Details` 필드에서 다음 보고 필드를 숨깁니다. `Ad Break ID`

      * `Media Collection Details` > `Chapter Details` 필드에서 보고 필드 `Chapter Completed`, `Chapter ID`, `Chapter Started` 및 `Chapter Time Played`을(를) 숨깁니다.

      * `Media Collection Details` 필드에서 `List Of States` 필드를 숨깁니다.

        ![미디어 컬렉션 상태 숨기기](assets/schema-hide-media-collection-states.png)

      * `Media Collection Details` > `List Of States End` 및 `Media Collection Details` > `List Of States Start` 필드에서 보고 필드 `Player State Count`, `Player State Set` 및 `Player State Time`을(를) 숨깁니다.

        ![숨길 필드](assets/schema-hide-listofstates.png)

      * `Media Collection Details` > `Qoe Data Details` 필드에서 보고 필드 `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Impacted Streams`, `Buffer Events`, `Dropped Frame Impacted Streams`, `Drops Before Starts`, `Errors`, `External Error IDs`, `Error Impacted Streams`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Impacted Streams`, `Stalling Events`, `Total Buffer Duration` 및 `Total Stalling Duration`을(를) 숨깁니다.

      * `Media Collection Details` > `Session Details` 필드에서 보고 필드 `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Completes`, `Chapter Count`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Segment Views`, `Media Downloaded Flag`, `Media Starts`, `Media Session ID`, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pev3`, `Pccr`, `Total Pause Duration`, `Unique Time Played` 및 `Video Segment`을(를) 숨깁니다.

   1. 변경 내용을 저장하려면 [!UICONTROL **확인**]&#x200B;을 선택하세요.

   1. [!UICONTROL **구조**] 영역에서 [!UICONTROL **필드에 대한 표시 이름을 표시**]&#x200B;하는 옵션을 활성화한 다음 `List Of Media Collection Downloaded Content Events` 필드를 선택합니다.

   1. [!UICONTROL **관련 필드 관리**]&#x200B;를 선택한 후 다음과 같이 스키마를 업데이트합니다.


      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` 필드에서 보고 필드 `Ad Completed`, `Ad Started` 및 `Ad Time Played`을(를) 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` 필드에서 다음 보고 필드를 숨깁니다. `Ad Break ID`

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` 필드에서 보고 필드 `Chapter Completed`, `Chapter ID`, `Chapter Started` 및 `Chapter Time Played`을(를) 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` 필드에서 `List Of States` 필드를 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` 및 `Media Collection Details` > `List Of States Start` 필드에서 보고 필드 `Player State Count`, `Player State Set` 및 `Player State Time`을(를) 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` 필드에서 보고 필드 `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Events`, `Buffer Impacted Streams`, `Drops Before Starts`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Errors`, `External Error IDs`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, `Stalling Impacted Streams`, `Total Buffer Duration` 및 `Total Stalling Duration`을(를) 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` 필드에서 보고 필드 `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Content Completes`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Media Segment Views`, `Media Session ID`, `Media Session Server Timeout`, `Media Starts`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pccr`, `Pev3`, `Total Pause Duration`, `Unique Time Played` 및 `Video Segment`을(를) 숨깁니다.

      * `List Of Media Collection Downloaded Content Events` > `Media Details` 필드에서 `Media Session ID` 필드를 숨깁니다.

   1. 변경 내용을 저장하려면 [!UICONTROL **확인**]&#x200B;을 선택하세요.

   1. [!UICONTROL **구조**] 영역에서 `Media Reporting Details` 필드를 선택하고 [!UICONTROL **관련 필드 관리**]&#x200B;를 선택합니다.

   1. [!UICONTROL **필드에 대한 표시 이름을 표시**]&#x200B;하는 옵션을 활성화한 다음 다음과 같이 스키마를 업데이트합니다.

      * `Media Reporting Details` 필드에서 `Error Details`, `List Of States End`, `List of States Start` 및 `Media Session ID` 필드를 숨깁니다.

   1. 변경 내용을 저장하려면 [!UICONTROL **확인**] > [!UICONTROL **저장**]&#x200B;을 선택합니다.

   +++

1. (선택 사항) 사용자 지정 메타데이터를 스키마에 추가할 수 있습니다. 이를 통해 특정 요구 사항 또는 컨텍스트에 맞게 사용자 정의할 수 있는 추가 사용자 정의 메타데이터를 포함할 수 있습니다. 이러한 유연성은 기존 스키마가 원하는 데이터 포인트를 다루지 않는 시나리오에서 유용합니다. (Media Edge API를 사용하여 사용자 지정 메타데이터로 작업할 수도 있습니다. 자세한 내용은 [Media Edge API를 사용하여 사용자 지정 메타데이터 만들기](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/custom-metadata/)를 참조하십시오.

   +++ 사용자 지정 메타데이터를 스키마에 추가하는 방법에 대한 지침을 보려면 여기를 확장하십시오.

   1. [!UICONTROL **계정 정보**] > [!UICONTROL **할당된 조직**] > [!UICONTROL _**조직 이름**_] > [!UICONTROL **테넌트**]&#x200B;를 선택하여 조직의 테넌트 이름을 찾습니다.

      이러한 사용자 정의 필드는 이 경로를 통해 수신됩니다. (예: 테넌트 이름: _dcbl → myCustomField 경로: _dcbl.myCustomField.)

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

   데이터 세트에 대한 스키마를 선택할 때는 [Adobe Experience Platform에서 스키마 설정](#set-up-the-schema-in-adobe-experience-platform)에 설명된 대로 이전에 만든 스키마를 선택합니다.

1. [Customer Journey Analytics에서 데이터 스트림 구성](#configure-a-datastream-in-adobe-experience-platform)을 계속합니다.

## Adobe Experience Platform에서 데이터 스트림 구성

1. [Adobe Experience Platform에서 데이터 세트 만들기](#create-a-dataset-in-adobe-experience-platform)에 설명된 대로 데이터 세트를 만들었는지 확인하십시오.

1. [데이터 스트림 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=ko)에 설명된 대로 새 데이터 스트림을 만듭니다.

   데이터 스트림을 생성할 때 다음 구성을 선택해야 합니다.

   * 데이터 스트림을 만들 때 [!UICONTROL **이벤트 스키마**] 필드에서 [Adobe Experience Platform에서 스키마를 설정](#set-up-the-schema-in-adobe-experience-platform)에서 만든 스키마를 선택했는지 확인하십시오. [!UICONTROL **저장**]&#x200B;을 선택합니다.

     >[!IMPORTANT]
     >
     >[!UICONTROL **매핑 저장 및 추가**]&#x200B;를 선택하지 마십시오. 그렇게 하면 타임스탬프 필드에 대한 매핑 오류가 발생합니다.

     ![데이터 스트림을 만들고 스키마 선택](assets/datastream-create-schema.png)

   * Adobe Analytics 또는 Customer Journey Analytics 사용 여부에 따라 데이터 스트림에 다음 서비스 중 하나를 추가합니다.

      * [!UICONTROL **Adobe Analytics**] (Adobe Analytics을 사용하는 경우)

        Adobe Analytics을 사용하는 경우 [보고서 세트 만들기](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite)에 설명된 대로 보고서 세트를 정의해야 합니다.

      * [!UICONTROL **Adobe Experience Platform**] (Customer Journey Analytics을 사용하는 경우)

     데이터 스트림에 서비스를 추가하는 방법에 대한 자세한 내용은 [데이터 스트림 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details)의 &quot;데이터 스트림에 서비스 추가&quot; 섹션을 참조하십시오.

     ![Adobe Analytics 서비스 추가](assets/datastream-add-service.png)

      * [!UICONTROL **고급 옵션**]&#x200B;을 확장한 다음 [!UICONTROL **Media Analytics**] 옵션을 활성화합니다.

     ![Media Analytics 옵션](assets/datastream-media-check.png)

1. 이제 Media Analytics 데이터 수집을 시작하려면 [Media Edge API](/help/implementation/edge/implementation-edge-api.md) 또는 [Media Edge SDK](/help/implementation/edge/edge-mobile-sdk.md)을(를) 구현할 준비가 되었습니다.

   일부 데이터를 수집한 후에는 [Customer Journey Analytics에서 연결을 만들 수 있습니다](#create-a-connection-in-customer-journey-analytics).

## Customer Journey Analytics에 연결 만들기

>[!NOTE]
>
>다음 절차는 Customer Journey Analytics을 사용하는 경우에만 필요합니다.

1. [Customer Journey Analytics에서 데이터 스트림 구성](#configure-a-datastream-in-adobe-experience-platform)에 설명된 대로 데이터 스트림을 만들었는지 확인하십시오.

1. [연결 만들기](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=ko-KR)에 설명된 대로 Customer Journey Analytics에서 연결을 만듭니다.

   연결을 만들 때 Streaming Media 컬렉션을 구현하려면 다음 구성 선택이 필요합니다.

   1. [Adobe Experience Platform에서 데이터 세트 만들기](#create-a-dataset-in-adobe-experience-platform)에 설명된 대로 이전에 만든 데이터 세트를 선택합니다.

   1. [!UICONTROL **새 데이터 모두 가져오기**] 설정이 활성화되어 있는지 확인하십시오.

1. [Customer Journey Analytics에서 데이터 보기 만들기](#create-a-new-data-view-in-customer-journey-analytics)를 계속합니다.

## Customer Journey Analytics에 데이터 보기 만들기

>[!NOTE]
>
>다음 절차는 Customer Journey Analytics을 사용하는 경우에만 필요합니다.

1. [Customer Journey Analytics에서 연결 만들기](#create-a-connection-in-customer-journey-analytics)에 설명된 대로 Customer Journey Analytics에서 연결을 만들었는지 확인하십시오.

1. 고객 여정 분석에서 [데이터 보기 만들기 또는 편집](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=ko-KR)에 설명된 대로 데이터 보기를 만듭니다.

   데이터 보기를 만들 때 Streaming Media 컬렉션을 구현하려면 다음 구성 선택이 필요합니다.

   1. [!UICONTROL **Customer Journey Analytics에서 연결 만들기**]&#x200B;에 설명된 대로 [연결](#create-a-connection-in-customer-journey-analytics) 필드에서 이전에 만든 연결을 선택합니다.

      생성한 연결을 선택할 수 있을 때까지 최대 15분이 소요될 수 있습니다.

   1. [!UICONTROL **구성 요소**] 탭의 [!UICONTROL **스키마 필드**] 섹션에서 아래 표에 나열된 각 구성 요소를 검색하여 [!UICONTROL **지표**] 패널로 드래그합니다. 동일한 이름의 필드가 여러 개 있는 경우 XDM 경로를 사용하여 필드가 올바른지 확인하십시오.

      **기본 콘텐츠 - 콘텐츠 지표**

      | 구성 요소 이름 | XDM 경로 |
      |----------|---------|
      | 미디어 시작 | mediaReporting.sessionDetails.isViewed |
      | 미디어 세그먼트 보기 수 | mediaReporting.sessionDetails.hasSegmentView |
      | 콘텐츠 시작 | mediaReporting.sessionDetails.isPlayed |
      | 컨텐츠 완료 | mediaReporting.sessionDetails.isCompleted |
      | 콘텐츠 체류 시간 | mediaReporting.sessionDetails.timePlayed |
      | 미디어 사용 시간 | mediaReporting.sessionDetails.totalTimePlayed |
      | 재생된 고유 시간 | mediaReporting.sessionDetails.uniqueTimePlayed |
      | 10% 진행률 마커 | mediaReporting.sessionDetails.hasProgress10 |
      | 대상자 분당 평균 시청 시간 | mediaReporting.sessionDetails.averageMinuteAudience |


      **챕터 및 광고 - 챕터 및 광고 지표**

      | 구성 요소 이름 | XDM 경로 |
      |----------|---------|
      | 챕터 시작됨 | mediaReporting.chapterDetails.isStarted |
      | 챕터 완료됨 | mediaReporting.chapterDetails.isCompleted |
      | 챕터 재생 시간 | mediaReporting.chapterDetails.timePlayed |
      | 광고 시작됨 | mediaReporting.advertisingDetails.isStarted |
      | 광고 완료됨 | mediaReporting.advertisingDetails.isCompleted |
      | 재생된 광고 시간 | mediaReporting.advertisingDetails.timePlayed |


      **QoE - QoE 지표**

      | 구성 요소 이름 | XDM 경로 |
      |----------|---------|
      | 시작 시간 | mediaReporting.qoeDataDetails.timeToStart |
      | 시작 전 드롭 | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | 버퍼 영향을 받은 스트림 | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | 비트율 변경의 영향을 받은 스트림 | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | 비트율 변경 | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | 평균 비트율 | mediaReporting.qoeDataDetails.bitrateAverage |
      | 드롭된 프레임 | mediaReporting.qoeDataDetails.droppedFrames |
      | 오류 | mediaReporting.qoeDataDetails.errorCount |
      | 오류 영향을 받은 스트림 | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | 드롭된 프레임 영향을 받은 스트림 | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |


      **플레이어 상태 - 플레이어 상태 지표**

      | 구성 요소 이름 | XDM 경로 |
      |----------|---------|
      | 플레이어 상태 집합 | mediaReporting.states.isSet |
      | 플레이어 상태 카운트 | mediaReporting.states.count |
      | 플레이어 상태 시간 | mediaReporting.states.time |


   1. 다음 표에서 구성 요소에 대한 레이블([!UICONTROL **컨텍스트 레이블**] 드롭다운 메뉴의)을 업데이트합니다. 지표 패널에 아직 없는 구성 요소를 검색하여 패널로 드래그합니다.

      | 구성 요소 이름 | 컨텍스트 레이블 |
      |---------|----------|
      | 미디어 세션 서버 시간 초과 | 미디어: 마지막 통화 이후 지난 시간(초) |
      | 미디어 사용 시간 | 미디어: 미디어 사용 시간 |
      | 총 버퍼 지속 시간 | 미디어: 총 버퍼 지속 시간 |
      | 시작 시간 | 미디어: 시작 시간 |
      | 총 일시 중지 기간 | 미디어: 총 일시 중단 기간 |

   1. Customer Journey Analytics 프로젝트에 분류를 추가하려면 [!UICONTROL **차원**] 패널에 다음 차원을 추가하십시오.

      | XDM 경로 | 구성 요소 이름 |
      |---------|----------|
      | mediaReporting.states.name | 플레이어 상태 이름 |
      | mediaReporting.sessionDetails.ID | 미디어 세션 ID |

      이 표의 차원 외에도, Customer Journey Analytics 프로젝트에서 데이터를 필터링하는 데 사용할 수 있도록 하려는 다른 차원에 추가할 수 있습니다.

1. 변경 내용을 저장하려면 [!UICONTROL **저장 후 계속**] > [!UICONTROL **저장 후 마침**]&#x200B;을 선택하십시오.

1. [Customer Journey Analytics에서 프로젝트 만들기 및 구성](#create-and-configure-a-project-in-customer-journey-analytics)을 계속합니다.

## Customer Journey Analytics에서 프로젝트 만들기 및 구성

1. [Customer Journey Analytics에서 데이터 보기 만들기](#create-a-new-data-view-in-customer-journey-analytics)에 설명된 대로 Customer Journey Analytics에서 데이터 보기를 만들었는지 확인하십시오.

1. Customer Journey Analytics의 [!UICONTROL **Workspace**] 탭의 [!UICONTROL **프로젝트**] 영역에서 [!UICONTROL **프로젝트 만들기**]&#x200B;를 선택합니다.

1. [!UICONTROL **빈 프로젝트**] > [!UICONTROL **만들기**]&#x200B;를 선택합니다.

1. 새 프로젝트에서 이전에 만든 데이터 보기를 선택합니다.

   프로젝트에서 패널을 만들 때 [Customer Journey Analytics에서 데이터 보기 만들기](#create-a-new-data-view-in-customer-journey-analytics)에 설명된 대로 데이터 보기에 추가한 구성 요소를 사용할 수 있습니다.

   다음 4개의 패널은 만들 수 있는 패널의 예입니다.

   ![기본 콘텐츠 패널](assets/main-content-panel.png)

   ![챕터 및 광고 패널](assets/chapter-and-ads-panel.png)

   ![QoE 패널](assets/qoe-panel.png)

   ![복사 상태 패널](assets/player-state-panel.png)

1. 왼쪽 레일에서 **패널** 아이콘을 선택한 다음 [!UICONTROL **미디어 동시 뷰어**] 패널과 [!UICONTROL **미디어 재생 소요 시간**] 패널에서 드래그합니다.

   2개의 패널은 다음과 같아야 합니다.

   ![미디어 동시 뷰어 패널](assets/media-concurrent-viewers-panels.png)

   ![미디어 재생 소요 시간 패널](assets/media-playback-time-spent-panels.png)

1. (조건부) [Adobe Experience Platform에서 스키마 설정](#set-up-the-schema-in-adobe-experience-platform)의 8단계에 설명된 대로 스키마에 사용자 지정 메타데이터를 추가한 경우 Customer Journey Analytics 안내서의 [지속성 구성 요소 설정](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)에 설명된 대로 사용자 지정 필드에 대한 지속성을 설정해야 합니다.

   데이터가 Customer Journey Analytics에 도착하면 사용자 지정 사용자 ID 차원을 사용할 수 있습니다.

   ![setup-custom-metadata](assets/custom-metadata-dimension.png)

   >[!NOTE]
   >
   >Adobe Analytics을 데이터 스트림의 업스트림으로 설정하는 경우, 사용자 지정 메타데이터는 스키마에서 설정한 이름과 함께 ContextData에도 표시됩니다(테넌트 접두사(예: myCustomField). 이렇게 하면 [처리 규칙 만들기](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules)와 같이 ContextData에 사용할 수 있는 모든 Adobe Analytics 기능을 사용할 수 있습니다.

1. [프로젝트 공유](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en)에 설명된 대로 프로젝트를 공유합니다.

   >[!NOTE]
   >
   >   공유하려는 사용자를 사용할 수 없는 경우 사용자에게 Adobe Admin Console의 Customer Journey Analytics에 대한 사용자 및 관리자 액세스 권한이 있는지 확인하십시오.


1. [Experience Platform Edge으로 데이터 보내기](#send-data-to-experience-platform-edge)를 계속합니다.

## Experience Platform Edge으로 데이터 보내기

Experience Platform Edge으로 전송할 데이터 유형에 따라 다음 방법 중 하나를 사용할 수 있습니다.

### 웹: Adobe Experience Platform 웹 SDK 사용

* [시작하기](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Adobe Experience Platform Web SDK을 사용하여 웹 데이터를 Edge으로 전송](/help/implementation/edge/edge-web-sdk.md)

* [Edge Network 확장 기능용 Adobe 스트리밍 미디어로 마이그레이션](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### 모바일: Adobe Experience Platform Mobile SDK 사용

다음 설명서 리소스를 사용하여 iOS 및 Android 모두에 대한 구현을 완료합니다.

* [시작하기](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [API 참조](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [Edge Network 확장 기능용 Adobe 스트리밍 미디어로 마이그레이션](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Roku: Adobe Experience Platform Roku SDK

* [시작하기](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main)

* [Edge Network 확장 기능용 Adobe Streaming Media로 마이그레이션](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/) <!-- is the information here also applicable for Roku? -->

### API: 웹 및 기타

API는 현재 웹 데이터를 Experience Platform Edge으로 전송하는 유일한 지원 방법입니다.

Edge API의 사용자 지정 구현을 사용하려는 경우에도 API를 사용할 수 있습니다.

Media Edge API에 대한 자세한 내용은 다음 리소스를 참조하십시오.

* [미디어 Edge API 개요](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html)

* [미디어 Edge API 시작](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html)

* [Media Edge API 문제 해결 안내서](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html)

* [Media Edge API에 대한 Open API 사양 파일 사용](https://developer.adobe.com/data-collection-apis/docs/api/media-edge/)
