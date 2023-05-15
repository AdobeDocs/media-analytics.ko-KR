---
title: 스트리밍 미디어용 Analytics에 대한 구현을 설정하는 첫 번째 단계입니다
description: Adobe 스트리밍 미디어를 구현하는 방법을 알아봅니다.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 723cfab6dd2d63448f44dc535724ffe4fd0ec8a7
workflow-type: tm+mt
source-wordcount: '1960'
ht-degree: 10%

---

# Experience Platform Edge로 Media Analytics 설치

Adobe Experience Platform Edge를 사용하면 여러 제품을 대상으로 한 데이터를 중앙 위치에 전송할 수 있습니다. Experience Edge는 적절한 정보를 원하는 제품에 전달합니다. 이 개념을 사용하면 특히 여러 데이터 솔루션에 걸쳐 구현 노력을 통합할 수 있습니다.

다음 그래픽은 Experience Platform Edge를 사용하는 Media Analytics 구현을 보여줍니다.

![Edge 구현](assets/media-analytics-implementation-overview.png)

>[!IMPORTANT]
>
>현재 Adobe Experience Platform Mobile SDK를 사용해야만 Experience Edge에 데이터를 보낼 수 있습니다.


<!-- Replace the above sentence with this after it web releases: You can send data to Experience Edge using any of the following implementation methods:

* Adobe Experience Platform Web SDK (Coming soon)
* Adobe Experience Platform Mobile SDK
* Edge Network Server API

Regardless of which Experience Edge implementation method you use for configuring media tracking, you must first complete the following sections:

-->

다음 섹션을 완료하여 Experience Platform Edge를 사용하여 Media Analytics를 구현합니다.

* [보고서 세트 정의](#define-a-report-suite)
* [Adobe Experience Platform에서 스키마 설정](#set-up-the-schema-in-adobe-experience-platform)
* [Adobe Experience Platform에서 데이터 세트 만들기](#create-a-dataset-in-adobe-experience-platform)
* [Adobe Experience Platform에서 데이터 스트림 구성](#configure-a-datastream-in-adobe-experience-platform)
* [Customer Journey Analytics에 연결 만들기](#create-a-connection-in-customer-journey-analytics)
* [Customer Journey Analytics에서 데이터 보기 만들기](#create-a-data-view-in-customer-journey-analytics)
* [Customer Journey Analytics에서 프로젝트 만들기 및 구성](#create-and-configure-a-project-in-customer-journey-analytics)
* [Edge 확장을 사용하여 Experience Platform Edge에 데이터 전송](#send-data-to-experience-platform-edge-with-the-edge-extension)

## 보고서 세트 정의

>[!NOTE]
>
>보고서 세트는 Adobe Analytics을 사용하는 경우에만 필요합니다. 보고에 Customer Journey Analytics을 사용하려는 경우에는 보고서 세트가 필요하지 않습니다.

보고에 Adobe Analytics을 사용하려는 경우 스트리밍 미디어 구현에 사용할 보고서 세트가 있어야 합니다. 보고서 세트 정의에 대한 자세한 내용은 [보고서 세트 관리자](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html?lang=en).

보고서 세트가 정의된 후 [Adobe Experience Platform에서 스키마 설정](#set-up-the-schema-in-adobe-experience-platform).

## Adobe Experience Platform에서 스키마 설정

Adobe Experience Platform을 활용하는 애플리케이션 전체에서 사용할 데이터 수집을 표준화하기 위해, Adobe는 개방적이고 공개적으로 문서화된 표준인 XDM(경험 데이터 모델)을 만들었습니다.

스키마를 생성 및 설정하려면 다음을 수행하십시오.

1. Adobe Experience Platform에서 에 설명된 대로 스키마 만들기를 시작합니다. [UI에서 스키마 만들기 및 편집](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

   스키마를 생성할 때 [!UICONTROL **XDM ExperienceEvent**] 에서 [!UICONTROL **스키마 만들기**] 드롭다운 메뉴

1. 에서 [!UICONTROL **조성물**] 영역, [!UICONTROL **필드 그룹**] 섹션, [!UICONTROL **추가**]&#x200B;를 검색하고 스키마에 다음 새 필드 그룹을 추가합니다.
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   필드 그룹을 추가한 후에는 [!UICONTROL **필드 그룹**] 섹션을 참조하십시오.

   ![필드 그룹을 추가했습니다](assets/schema-field-groups-added.png)

1. 에서 [!UICONTROL **구조**] 영역을 선택하고 `endUserIds` > `_experience` 필드 그룹을 선택한 다음 [!UICONTROL **관련 필드 관리**].

   ![관련 필드 관리 단추](assets/manage-related-fields.png)

1. 다음과 같이 스키마를 업데이트합니다.

   * 에서 `Adobe Analytics ExperienceEvent Template` 필드 그룹, 다음을 제외한 모든 필드 숨기기 `EndUserIDs`.

   * 에서 `endUserIds` > `_experience` > `Adobe Advertising Cloud end user IDs` 필드 그룹, 필드를 제외한 모든 필드 숨기기 `Identifier` 필드.

   * 에서 `endUserIds` > `_experience` > `Adobe Analytics Cloud Custom end user IDs` 필드 그룹, 필드를 제외한 모든 필드 숨기기 `Identifier` 필드.

      ![숨길 필드](assets/schema-hide-fields.png)

1. 선택 [!UICONTROL **확인**] 변경 사항을 저장하려면 을 클릭합니다.

1. 에서 [!UICONTROL **구조**] 영역을 선택하고 `Implementation Details` 필드 그룹, 선택 [!UICONTROL **관련 필드 관리**]&#x200B;를 업데이트한 후 다음과 같이 스키마를 업데이트합니다.

   * 에서 `Implementation Details` > `Implementation details` 필드 그룹, 다음을 제외한 모든 필드 숨기기 `version`.

      ![숨길 필드](assets/schema-hide-fields2.png)

1. 선택 [!UICONTROL **확인**] 변경 사항을 저장하려면 을 클릭합니다.

1. 에서 [!UICONTROL **구조**] 영역을 선택하고 `Media Collection Details` 필드 그룹, 선택 [!UICONTROL **관련 필드 관리**]&#x200B;를 업데이트한 후 다음과 같이 스키마를 업데이트합니다.

   * 에서 `Media Collection Details` 필드 그룹, 숨기기 `List Of States` 필드 그룹.

      ![미디어 컬렉션 상태 숨기기](assets/schema-hide-media-collection-states.png)

   * 에서 `Media Collection Details` > `Advertising Details` 필드 그룹, 다음 보고 필드를 숨깁니다. `Ad Completed`, `Ad Started`, 및 `Ad Time Played`.

   * 에서 `Media Collection Details` > `Advertising Pod Details` 필드 그룹, 다음 보고 필드를 숨깁니다. `Ad Break ID`

   * 에서 `Media Collection Details` > `Chapter Details` 필드 그룹에서 다음 보고 필드를 숨깁니다. `Chapter ID`, `Chapter Completed`, `Chapter Started`, 및 `Chapter Time Played`.

   * 에서 `Media Collection Details` > `Qoe Data Details` 필드 그룹에서 다음 보고 필드를 숨깁니다. `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, 및 `Total Stalling Duration`.

   * 에서 `Media Collection Details` > `Session Details` 필드 그룹에서 다음 보고 필드를 숨깁니다. `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`, 및 `Pccr`.

   * 에서 `Media Collection Details` > `List Of States End` 및 `Media Collection Details` > `List Of States Start` 필드 그룹, 다음 보고 필드를 숨깁니다. `Player State Count`, `Player State Set`, 및 `Player State Time`.

      ![숨길 필드](assets/schema-hide-listofstates.png)

1. 선택 [!UICONTROL **확인**] 변경 사항을 저장하려면 을 클릭합니다.

1. 에서 [!UICONTROL **구조**] 영역을 선택하고 `List Of Media Collection Downloaded Content Events` 필드 그룹, 선택 [!UICONTROL **관련 필드 관리**]&#x200B;를 업데이트한 후 다음과 같이 스키마를 업데이트합니다.

   * 에서 `List Of Media Collection Downloaded Content Events` > `Media Details` 필드 그룹, 숨기기 `List Of States` 필드 그룹.

   * 에서 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` 필드 그룹, 다음 보고 필드를 숨깁니다. `Ad Completed`, `Ad Started`, 및 `Ad Time Played`.

   * 에서 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` 필드 그룹, 다음 보고 필드를 숨깁니다. `Ad Break ID`

   * 에서 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` 필드 그룹에서 다음 보고 필드를 숨깁니다. `Chapter ID`, `Chapter Completed`, `Chapter Started`, 및 `Chapter Time Played`.

   * 에서 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` 필드 그룹에서 다음 보고 필드를 숨깁니다. `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, 및 `Total Stalling Duration`.

   * 에서 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` 필드 그룹에서 다음 보고 필드를 숨깁니다. `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`, 및 `Pccr`.

   * 에서 `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` 및 `Media Collection Details` > `List Of States Start` 필드 그룹, 다음 보고 필드를 숨깁니다. `Player State Count`, `Player State Set`, 및 `Player State Time`.

   * 에서 `List Of Media Collection Downloaded Content Events` > `Media Details`  필드 그룹, 숨기기 `Media Session ID` 필드.

1. 선택 [!UICONTROL **확인**] 변경 사항을 저장하려면 을 클릭합니다.

1. 에서 [!UICONTROL **구조**] 영역을 선택하고 `Media Reporting Details` 필드 그룹, 선택 [!UICONTROL **관련 필드 관리**]&#x200B;를 업데이트한 후 다음과 같이 스키마를 업데이트합니다.

   * 에서 `Media Reporting Details` 필드 그룹, 다음 필드 그룹을 숨깁니다. `Error Details`, `List Of States End`, `List of States Start`, `Playhead`, 및 `Media Session ID`.

1. 선택 [!UICONTROL **확인**] > [!UICONTROL **저장**]  변경 사항을 저장하려면 을 클릭합니다.

1. 계속 [Adobe Experience Platform에서 데이터 세트 만들기](#create-a-dataset-in-adobe-experience-platform).

## Adobe Experience Platform에서 데이터 세트 만들기

1. 에 설명된 대로 스키마를 설정해야 합니다. [Adobe Experience Platform에서 스키마 설정](#set-up-the-schema-in-adobe-experience-platform).

1. Adobe Experience Platform에서 다음에 설명된 대로 데이터 세트 만들기를 시작합니다. [데이터 세트 UI 안내서](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=ko#create).

   데이터 세트에 대한 스키마를 선택할 때 다음에 설명된 대로, 이전에 만든 스키마를 선택합니다 [Adobe Experience Platform에서 스키마 설정](#set-up-the-schema-in-adobe-experience-platform).

1. 계속 [Customer Journey Analytics에서 데이터 스트림 구성](#configure-a-datastream-in-adobe-experience-platform).

## Adobe Experience Platform에서 데이터 스트림 구성

1. 에 설명된 대로 데이터 세트를 만들었는지 확인합니다. [Adobe Experience Platform에서 데이터 세트 만들기](#create-a-dataset-in-adobe-experience-platform).

1. 에 설명된 대로 새 데이터 스트림을 만듭니다. [데이터 스트림 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=ko-KR).

   데이터 스트림을 만들 때 다음 구성을 선택해야 합니다.

   * 에서 [!UICONTROL **이벤트 스키마**] 필드에서는 데이터 스트림을 만들 때 생성한 스키마를 선택해야 합니다 [Adobe Experience Platform에서 스키마 설정](#set-up-the-schema-in-adobe-experience-platform). [!UICONTROL **저장**]&#x200B;을 선택합니다.

      >[!IMPORTANT]
          >
      > 선택하지 않음 [!UICONTROL **매핑 저장 및 추가**] 이렇게 하면 타임스탬프 필드에 대한 매핑 오류가 발생합니다.
      

      ![데이터 스트림 만들기 및 스키마 선택](assets/datastream-create-schema.png)

   * Adobe Analytics 또는 Customer Journey Analytics 사용 여부에 따라 다음 서비스 중 하나를 데이터 스트림에 추가합니다.

      * [!UICONTROL **Adobe Analytics**] (Adobe Analytics을 사용하는 경우)

         Adobe Analytics을 사용하는 경우 섹션에 설명된 대로 보고서 세트를 정의해야 합니다 [보고서 세트 정의](#define-a-report-suite) 참조하십시오.

      * [!UICONTROL **Adobe Experience Platform**] (Customer Journey Analytics을 사용하는 경우)
      데이터 스트림에 서비스를 추가하는 방법에 대한 자세한 내용은 의 &quot;데이터 스트림에 서비스 추가&quot; 섹션을 참조하십시오. [데이터 스트림 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

      ![Adobe Analytics 서비스 추가](assets/datastream-add-service.png)

   * 확장 [!UICONTROL **고급 옵션**]&#x200B;를 활성화한 후 [!UICONTROL **Media Analytics**] 선택 사항입니다.

      ![Media Analytics 옵션](assets/datastream-media-check.png)


1. 계속 [Customer Journey Analytics에서 연결 만들기](#create-a-connection-in-customer-journey-analytics).

## Customer Journey Analytics에 연결 만들기

>[!NOTE]
>
>다음 절차는 Customer Journey Analytics을 사용하는 경우에만 필요합니다.


1. 다음에 설명된 대로 데이터 스트림을 생성했는지 확인합니다. [Customer Journey Analytics에서 데이터 스트림 구성](#configure-a-datastream-in-adobe-experience-platform).

1. Customer Journey Analytics에서 에 설명된 대로 연결을 만듭니다. [연결 만들기](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=ko-KR).

   연결을 만들 때 스트리밍 미디어를 구현하려면 다음 구성을 선택해야 합니다.

   1. 에 설명된 대로 이전에 만든 데이터 세트를 선택합니다 [Adobe Experience Platform에서 데이터 세트 만들기](#create-a-dataset-in-adobe-experience-platform).

   1. 다음을 확인합니다. [!UICONTROL **모든 새 데이터 가져오기**] 이 활성화되어 있습니다.

1. 계속 [Customer Journey Analytics에서 데이터 보기 만들기](#create-a-new-data-view-in-customer-journey-analytics).

## Customer Journey Analytics에서 데이터 보기 만들기

>[!NOTE]
>
>다음 절차는 Customer Journey Analytics을 사용하는 경우에만 필요합니다.

1. 에 설명된 대로 Customer Journey Analytics에서 연결을 만들었는지 확인합니다. [Customer Journey Analytics에서 연결 만들기](#create-a-connection-in-customer-journey-analytics).

1. 고객 여정 분석에서 에 설명된 대로 데이터 보기를 만듭니다. [데이터 보기 만들기 또는 편집](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=ko-KR).

   데이터 보기를 만들 때 스트리밍 미디어를 구현하려면 다음 구성을 선택해야 합니다.

   1. 에서 [!UICONTROL **연결**] 필드에서 에 설명된 대로 이전에 만든 연결을 선택합니다. [Customer Journey Analytics에서 연결 만들기](#create-a-connection-in-customer-journey-analytics).

      만든 연결을 선택하려면 최대 15분이 걸릴 수 있습니다.

   1. 설정 [!UICONTROL **구성 요소**] 탭, [!UICONTROL **스키마 필드**] 섹션에서 아래 표에 나열된 각 구성 요소를 검색하여 [!UICONTROL **지표**] 패널. 동일한 이름의 필드가 여러 개 있는 경우 XDM 경로를 사용하여 올바른 필드인지 확인하십시오.

      **기본 컨텐츠 - 컨텐츠 지표**

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


      **장 및 광고 - 장 및 광고 지표**

      | 구성 요소 이름 | XDM 경로 |
      |----------|---------|
      | 시작 장 | mediaReporting.chapterDetails.isStarted |
      | 장 완료 | mediaReporting.chapterDetails.isCompleted |
      | 장 재생 시간 | mediaReporting.chapterDetails.timePlayed |
      | 광고 시작됨 | mediaReporting.advertisingDetails.isStarted |
      | 광고 완료 | mediaReporting.advertisingDetails.isCompleted |
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
      | 플레이어 상태 수 | mediaReporting.states.count |
      | 플레이어 상태 시간 | mediaReporting.states.time |


   1. 레이블을 업데이트합니다( [!UICONTROL **컨텍스트 레이블**] 드롭다운 메뉴)를 클릭하여 제품에서 사용할 수 있습니다. 지표 패널에 아직 없는 구성 요소를 검색하여 패널로 드래그합니다.

      | 구성 요소 이름 | 컨텍스트 레이블 |
      |---------|----------|
      | 미디어 세션 서버 시간 초과 | 미디어: 마지막 호출 이후 시간(초) |
      | 미디어 사용 시간 | 미디어: 미디어 체류 시간 |
      | 총 버퍼 지속 시간 | 미디어: 총 버퍼 지속 시간 |
      | 시작 시간 | 미디어: 시작 시간 |
      | 총 일시 중지 기간 | 미디어: 총 일시 중지 기간 |

   1. Customer Journey Analytics 프로젝트에 분류를 추가하려면 다음 차원을 [!UICONTROL **Dimension**] 패널:

      | XDM 경로 | 구성 요소 이름 |
      |---------|----------|
      | mediaReporting.states.name | 플레이어 상태 이름 |
      | mediaReporting.sessionDetails.ID | 미디어 세션 ID |

      이 테이블의 차원 외에도 Customer Journey Analytics 프로젝트에서 데이터를 필터링하는 데 사용할 수 있도록 하려는 다른 차원에도 추가할 수 있습니다.

1. 선택 [!UICONTROL **저장 후 계속**] > [!UICONTROL **저장 및 완료**] 변경 사항을 저장하려면 을 클릭합니다.

1. 계속 [Customer Journey Analytics에서 프로젝트 만들기 및 구성](#create-and-configure-a-project-in-customer-journey-analytics).

## Customer Journey Analytics에서 프로젝트 만들기 및 구성

1. 에 설명된 대로 Customer Journey Analytics에서 데이터 보기를 만들었는지 확인합니다. [Customer Journey Analytics에서 데이터 보기 만들기](#create-a-new-data-view-in-customer-journey-analytics).

1. Customer Journey Analytics에서 [!UICONTROL **작업 공간**] 탭, [!UICONTROL **프로젝트**] 영역, 선택 [!UICONTROL **프로젝트 만들기**].

1. 선택 [!UICONTROL **빈 프로젝트**] > [!UICONTROL **만들기**].

1. 새 프로젝트에서 이전에 만든 데이터 보기를 선택합니다.

   프로젝트에서 패널을 만들 때 다음에 설명된 대로 데이터 보기에 추가한 구성 요소를 사용할 수 있습니다. [Customer Journey Analytics에서 데이터 보기 만들기](#create-a-new-data-view-in-customer-journey-analytics).

   다음 4개의 패널은 만들 수 있는 패널의 예입니다.

   ![기본 컨텐츠 패널](assets/main-content-panel.png)

   ![장 및 광고 패널](assets/chapter-and-ads-panel.png)

   ![QoE 패널](assets/qoe-panel.png)

   ![플레이터 상태 패널](assets/player-state-panel.png)

1. 을(를) 선택합니다 **패널** 왼쪽 레일의 아이콘을 클릭한 다음 [!UICONTROL **미디어 Concurrent Viewer**] 패널 및 [!UICONTROL **미디어 재생 시간**] 패널.

   두 패널은 다음과 같습니다.

   ![미디어 동시 뷰어 패널](assets/media-concurrent-viewers-panels.png)

   ![미디어 재생 시간 패널](assets/media-playback-time-spent-panels.png)

1. 에 설명된 대로 프로젝트를 공유합니다. [프로젝트 공유](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >   공유할 사용자를 사용할 수 없는 경우 Adobe Admin Console에서 Customer Journey Analytics에 대한 사용자 및 관리자 액세스 권한이 있는지 확인하십시오.

1. 계속 [Experience Platform Edge에 데이터 보내기](#send-data-to-experience-platform-edge).

## AEP Mobile SDK를 사용하여 데이터를 Edge로 전송

Adobe Experience Platform Mobile SDK를 사용하여 모바일 데이터를 Experience Platform Edge로 전송할 수 있습니다. (또는 에지 API의 사용자 지정 구현을 사용할 수 있습니다.)<!-- I guess we don't need/want to document this? -->)

다음 설명서 리소스를 사용하여 구현을 완료합니다.


| 모바일 운영 체제 | 리소스 |
|---------|----------|
| **iOS** | iOS 모바일 데이터를 전송하는 데 다음 리소스를 사용할 수 있습니다. <ul><li>[데이터 수집 UI를 사용하여 Mobile SDK 구성](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/getting-started.md)</li><li>[Media SDK에서 Edge Media SDK로 마이그레이션](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/migration-guide.md)</li><li>[Edge Media API 참조](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/api-reference.md)</li></ul> |
| **Android** | Android 모바일 데이터를 전송하는 데 다음 리소스를 사용할 수 있습니다. <ul><li>[데이터 수집 UI를 사용하여 Mobile SDK 구성](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/getting-started.md)</li><li>[Media SDK에서 Edge Media SDK로 마이그레이션](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/migration-guide.md)</li><li>[Edge Media API 참조](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/api-reference.md)</li></ul> |


<!--

+++Adobe Experience Platform Mobile SDK

If you plan to use the Mobile SDK extension in Adobe Experience Platform Data Collection to send data to Edge, complete the following sections:

### Create a mobile property

Create a mobile property, as described in [Set up a mobile property](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/). 

Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/mobile-sdk/overview.html?lang=en 

The Adobe Experience Platform Mobile SDK helps power Adobe's Experience Cloud solutions and services in your mobile apps. It is available for Android, iOS, and various cross-platform development frameworks. Configuration is handled through Adobe Experience Platform Data Collection.
>[!IMPORTANT]
>
>An Adobe Analytics extension is also available in Adobe Experience Platform Data Collection. If you install this extension, you do not take advantage of XDM or the Edge Network.

### Register the extensions and load your tag configuration

Use code in your app to register the necessary extensions and load your tag configuration. For more information, see [Set up the configuration](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration) in [Getting started with Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration).

### Implement and test fuctionality

Implement and test app functionality using a combination of tags data elements, rules, additional extensions, and SDK API calls. Inspect, validate, and debug data collection and experiences for your mobile application.

For more information, see [Use the sample application](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application) in [Getting started with Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration).

### Extend and validate your mobile app implementation

Before pushing the mobile app extension to your production environment, first validate that it works.

(What are the steps to do this?)

-->

<!--

+++Adobe Experience Platform Web SDK (Coming soon)

>[!NOTE]
>
>The Adobe Experience Platform Web SDK is not yet available. This page will be updated when it becomes available.

<!-- Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/web-sdk/overview.html?lang=en -->

<!-- Use the Web SDK extension in Adobe Experience Platform Data Collection to send data to Edge.

You can use the [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/sdk/overview.html) to send data to Adobe Analytics. This implementation method works by translating the [Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html) into a format used by Analytics.

You can send data to Experience Edge directly using the Web SDK, or through the Web SDK extension in Tags. -->

<!-- ### Web SDK

A high-level overview of the implementation tasks:

![Implement Adobe Analytics using Web SDK workflow](../../assets/websdk-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Create a data layer</b> to manage the tracking of the data on your website.</td>
<td><a href="../../prepare/data-layer.md">Create a data layer</a></td>
</tr>

<tr>
<td> 4</td>
<td><b>Install the prebuilt standalone version</b>. You can reference the library (<code>alloy.js</code>) on the CDN directly on your page or download and host it on your own infrastructure. Alternatively, you can use the NPM package.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=en#option-2%3A-installing-the-prebuilt-standalone-version">Installing the prebuilt standalone version</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=en#option-3%3A-using-the-npm-package">Using the NPM package</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<td>6</td>
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>7</td>
<td><b>Configure the Web SDK</b>. Ensure the library that you installed in step 4 is properly configured with the datastream ID (formerly known as edge configuration id (<code>edgeConfigId</code>)), organization id (<code>orgId</code>), and other available options.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en">Configure the Web SDK</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Execute commands</b> and/or <b>track events</b>. After the base code has been implemented on your webpage, you can begin executing commands and tracking events with the SDK.
</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/executing-commands.html?lang=en">Execute commands</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en">Track events</a></td>
</tr>

<tr>
<td>9</td><td><b>Extend and validate your implementation</b> before pushing it out to production.</td><td></td> 
</tr>
</table>


### Web SDK extension

A high-level overview of the implementation tasks:

![Implement Adobe Analytics using Web SDK extension workflow](../../assets/websdk-extension-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Create a data layer</b> to manage the tracking of the data on your website.</td>
<td><a href="../../prepare/data-layer.md">Create a data layer</a></td>
</tr>

<tr>
<td>4</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<tr>
<td>5</td> 
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>6</td>
<td><b>Create a tag property</b>. Properties are overarching containers used to reference tag management data.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=en#for-web">Create or configure a tag property for web</a></td>
</tr>

<tr>
<td>7</td> 
<td><b>Install and configure the Web SDK extension</b> in your tag property. Configure the Web SDK extension to send data to the datastream configured in step 4.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/sdk/overview.html?lang=en">Adobe Experience Platform Web SDK extension overview</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Iterate, validate, and publish</b> to production. Add the tag property to your web site. Then use data elements, rules, and so on, to customize your implementation.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=en">Publishing overview</a></td>
</tr>

</table>


### Additional resources

Tags can be highly customized. Learn more about how you can get the most out of Adobe Analytics by including the right data in your implementation.

-   [Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html#): Learn how the interface works and what extensions are available.

-   [Adobe Experience Platform Web SDK documentation](https://experienceleague.adobe.com/docs/web-sdk.html?lang=en)


+++

-->


<!--

### Adobe Experience Platform SDK

A high-level overview of the implementation tasks:

![Adobe Analytics using the Analytics extension workflow](../../assets/mobilesdk-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<td>4</td>
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Create a mobile property</b>. A property is a container that you fill with extensions, rules, data elements, and libraries.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/">Set up a mobile property</a></tr>

<tr>
<td>6</td>
<td><b>Install the Adobe Experience Platform Edge Network extension</b> in the mobile tag property and configure the datastream in the extension.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/edge-network/">Adobe Experience Platform Edge Network</a>
</tr>

<tr>
<td>7</td>
<td><b>Use code in your app</b> to register the necessary extensions and load your tag configuration.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration">Set up the configuration</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Implement and test functionality</b> using combination of tag's data elements, rules, additional extensions, and SDK API calls in your app. Inspect, validate, and debug data collection and experiences for your mobile application.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application">Use the sample application</a>
</tr>

<tr>
<td>9</td>
<td><b>Extend and validate your mobile app implementation</b> before pushing it out to production.</td>
<td></td> 
</tr>

</table>


### Adobe Analytics extension.

A high-level overview of the implementation tasks:

![Adobe Analytics using the Analytics extension workflow](../../assets/mobilesdk-analytics-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Install the Adobe Analytics extension</b> in the mobile tag property and configure the extension to point to your report suite.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/adobe-analytics/">Adobe Analytics extension for mobile property</a>
</tr>

<tr>
<td>4</td>
<td><b>Use code in your app</b> to register the necessary extensions and load your tag configuration.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration">Set up the configuration</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Implement and test functionality</b> using combination of tag's data elements, rules, additional extensions, and SDK API calls in your app. Inspect, validate, and debug data collection and experiences for your mobile application.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application">Use the sample application</a>
</tr>

<tr>
<td>6</td>
<td><b>Extend and validate your mobile app implementation</b> before pushing it out to production.</td>
<td></td> 
</tr>

</table>

### Additional resources

-   [Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html#)

-   [Mobile SDK documentation](https://developer.adobe.com/client-sdks/documentation/)

-->

<!--

+++

+++Edge Network Server API

Send data directly to Edge using an API.

Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/edge-api/overview.html?lang=en 

If you are unable to use the Adobe Experience Platform [Web SDK](../web-sdk/overview.md) or [Mobile SDK](../mobile-sdk/overview.md), you can send data to the Edge Network directly through an API.

See [Edge Network Server API documentation](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html), and an example [integrating with Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/interacting-other-adobe-solutions/interacting-adobe-analytics.html).

+++ 

-->

