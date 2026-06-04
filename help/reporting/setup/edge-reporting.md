---
title: Edge 구현에 대한 보고 설정
description: Edge Network을 통해 수집된 스트리밍 미디어 데이터에 대해 보고하도록 Customer Journey Analytics을 구성합니다.
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 17%

---

# Edge 구현에 대한 보고 설정

Edge Network을 통해 스트리밍 미디어 컬렉션을 구현한 후 수집된 데이터에 대해 보고하도록 Customer Journey Analytics을 구성합니다. 이 페이지에서는 스트리밍 미디어용 연결, 데이터 보기 및 프로젝트를 만드는 방법을 설명합니다.

>[!NOTE]
>
>이 페이지에서는 Edge 구현에 대한 권장 대상인 Customer Journey Analytics의 보고에 대해 설명합니다. 데이터 스트림이 스트리밍 미디어 데이터를 대신 Adobe Analytics으로 보내는 경우 [Analytics 전용 구현에 대한 보고 설정](analytics-reporting.md)을 참조하십시오.

* **필수 구성 요소**: Edge 구현을 완료하고 일부 데이터를 수집합니다. [Edge 구현 개요](/help/implementation/edge/overview.md) 및 선택한 구현 방법을 참조하십시오.

## Customer Journey Analytics에 연결 만들기

1. [연결 만들기](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=ko-KR)에 설명된 대로 Customer Journey Analytics에서 연결을 만듭니다.

   연결을 만들 때 스트리밍 미디어에 대해 다음 선택이 필요합니다.

   1. 구현 중에 만든 데이터 세트를 선택합니다.

   1. **[!UICONTROL 새 데이터 모두 가져오기]** 설정이 활성화되어 있는지 확인하십시오.

1. [Customer Journey Analytics에서 데이터 보기 만들기](#create-a-data-view-in-customer-journey-analytics)를 계속합니다.

## Customer Journey Analytics에 데이터 보기 만들기

1. [데이터 보기 만들기 또는 편집](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=ko-KR)에 설명된 대로 Customer Journey Analytics에서 데이터 보기를 만듭니다.

   1. **[!UICONTROL 연결]** 필드에서 이전에 만든 연결을 선택합니다.

      새 연결을 선택하려면 최대 15분이 걸릴 수 있습니다.

   1. **[!UICONTROL 구성 요소]** 탭의 **[!UICONTROL 스키마 필드]** 섹션에서 아래 표에서 각 구성 요소를 검색하여 **[!UICONTROL 지표]** 패널로 드래그합니다. 동일한 이름의 필드가 여러 개 있는 경우 XDM 경로를 사용하여 올바른 필드를 확인하십시오.

      **기본 콘텐츠 - 콘텐츠 지표**

      | 구성 요소 이름 | XDM 경로 |
      |----------|---------|
      | 미디어 시작 | mediaReporting.sessionDetails.isViewed |
      | 미디어 세그먼트 보기 수 | mediaReporting.sessionDetails.hasSegmentView |
      | 콘텐츠 시작 | mediaReporting.sessionDetails.isPlay |
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
      | 광고 재생 시간 | mediaReporting.advertisingDetails.timePlayed |

      **QoE - QoE 지표**

      | 구성 요소 이름 | XDM 경로 |
      |----------|---------|
      | 시작 시간 | mediaReporting.qoeDataDetails.timeToStart |
      | 시작 전 드롭 | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | 버퍼 영향을 받은 스트림 | mediaReporting.qoeDataDetails.hasBufferImpactStreams |
      | 비트율 변경의 영향을 받은 스트림 | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | 비트율 변경 | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | 평균 비트율 | mediaReporting.qoeDataDetails.bitrateAverage |
      | 드롭된 프레임 | mediaReporting.qoeDataDetails.droppedFrames |
      | 오류 | mediaReporting.qoeDataDetails.errorCount |
      | 오류 영향을 받은 스트림 | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | 드롭된 프레임 영향을 받은 스트림 | mediaReporting.qoeDataDetails.hasDropFrameImpactedStreams |

      **플레이어 상태 - 플레이어 상태 지표**

      | 구성 요소 이름 | XDM 경로 |
      |----------|---------|
      | 플레이어 상태 집합 | mediaReporting.states.isSet |
      | 플레이어 상태 카운트 | mediaReporting.states.count |
      | 플레이어 상태 시간 | mediaReporting.states.time |

   1. 다음 표에서 구성 요소에 대한 레이블(**[!UICONTROL 컨텍스트 레이블]** 드롭다운 메뉴의)을 업데이트합니다. 지표 패널에 아직 없는 구성 요소를 검색하여 패널로 드래그합니다.

      | 구성 요소 이름 | 컨텍스트 레이블 |
      |---------|----------|
      | 미디어 세션 서버 시간 초과 | 미디어: 마지막 통화 이후 지난 시간(초) |
      | 미디어 사용 시간 | 미디어: 미디어 사용 시간 |
      | 총 버퍼 지속 시간 | 미디어: 총 버퍼 지속 시간 |
      | 시작 시간 | 미디어: 시작 시간 |
      | 총 일시 중지 기간 | 미디어: 총 일시 중단 기간 |

   1. 분류를 프로젝트에 추가하려면 **[!UICONTROL 차원]** 패널에 다음 차원을 추가하십시오.

      | XDM 경로 | 구성 요소 이름 |
      |---------|----------|
      | mediaReporting.states.name | 플레이어 상태 이름 |
      | mediaReporting.sessionDetails.ID | 미디어 세션 ID |

      이 테이블의 차원 외에도 프로젝트에서 데이터를 필터링할 다른 차원을 추가할 수 있습니다.

1. 변경 내용을 저장하려면 **[!UICONTROL 저장 후 계속]** > **[!UICONTROL 저장 후 마침]**&#x200B;을 선택하십시오.

1. [Customer Journey Analytics에서 프로젝트 만들기 및 구성](#create-and-configure-a-project-in-customer-journey-analytics)을 계속합니다.

## Customer Journey Analytics에서 프로젝트 만들기 및 구성

1. Customer Journey Analytics의 **[!UICONTROL Workspace]** 탭의 **[!UICONTROL 프로젝트]** 영역에서 **[!UICONTROL 프로젝트 만들기]**&#x200B;를 선택합니다.

1. **[!UICONTROL 빈 프로젝트]** > **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

1. 새 프로젝트에서 이전에 만든 데이터 보기를 선택합니다.

   프로젝트에서 패널을 만들 때 데이터 보기에 추가한 구성 요소를 사용할 수 있습니다.

1. 왼쪽 레일에서 **패널** 아이콘을 선택한 다음 **[!UICONTROL 미디어 동시 뷰어]** 패널과 **[!UICONTROL 미디어 재생 소요 시간]** 패널에서 드래그합니다.

1. (조건부) 사용자 지정 메타데이터를 스키마에 추가한 경우 Customer Journey Analytics 안내서의 [지속성 구성 요소 설정](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)에 설명된 대로 사용자 지정 필드의 지속성을 설정하십시오.

1. [프로젝트 공유](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en)에 설명된 대로 프로젝트를 공유합니다.

   >[!NOTE]
   >
   >공유하려는 사용자를 사용할 수 없는 경우 사용자에게 Adobe Admin Console의 Customer Journey Analytics에 대한 사용자 및 관리자 액세스 권한이 있는지 확인하십시오.

>[!MORELIKETHIS]
>
>* [Workspace의 미디어 패널](/help/reporting/workspace/media-concurrent-viewers-overview.md)
>* [차원 개요](/help/reporting/dimensions/overview.md)
>* [지표 개요](/help/reporting/metrics/overview.md)
