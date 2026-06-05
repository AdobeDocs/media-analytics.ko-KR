---
title: Edge 구현에 대한 보고 설정
description: Edge Network을 통해 수집된 스트리밍 미디어 데이터에 대해 보고하도록 Customer Journey Analytics을 구성합니다.
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 6%

---

# Edge 구현에 대한 보고 설정

Edge Network을 통해 스트리밍 미디어 컬렉션을 구현한 후 수집된 데이터에 대해 보고하도록 Customer Journey Analytics을 구성합니다.

>[!NOTE]
>
>이 페이지에서는 Edge 구현에 대한 권장 대상인 Customer Journey Analytics의 보고에 대해 설명합니다. 데이터 스트림이 스트리밍 미디어 데이터를 대신 Adobe Analytics으로 보내는 경우 [Analytics 전용 구현에 대한 보고 설정](analytics-reporting.md)을 참조하십시오.

* **필수 구성 요소**: Edge 구현을 완료하고 일부 데이터를 수집합니다. [Edge 구현 개요](/help/implementation/edge/overview.md) 및 선택한 구현 방법을 참조하십시오.

## Customer Journey Analytics에 연결 만들기

1. [연결 만들기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-connections/create-connection)에 설명된 대로 Customer Journey Analytics에서 연결을 만듭니다. 연결을 만들 때 **[!UICONTROL 새 데이터 모두 가져오기]** 확인란이 활성화되어 있는지 확인하십시오.

## Customer Journey Analytics에 데이터 보기 만들기

1. [데이터 보기 만들기 또는 편집](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/create-dataview)에 설명된 대로 Customer Journey Analytics에서 데이터 보기를 만듭니다.

   1. **[!UICONTROL 연결]** 필드에서 이전에 만든 연결을 선택합니다. 새 연결이 표시되는 데 최대 15분이 소요될 수 있습니다.

   1. **[!UICONTROL 구성 요소]** 탭의 **[!UICONTROL 스키마 필드]** 섹션에서 아래 표의 각 구성 요소를 검색하여 적절한 **[!UICONTROL 차원]** 또는 **[!UICONTROL 지표]** 패널로 드래그합니다. 동일한 이름의 필드가 여러 개 있는 경우 XDM 경로를 사용하여 올바른 필드를 확인하십시오. 구성 요소 설정의 **[!UICONTROL 컨텍스트 레이블]** 드롭다운에 표시된 컨텍스트 레이블을 적용합니다.

      | 구성 요소 | 유형 | XDM 경로 | 컨텍스트 레이블 |
      |---|---|---|---|
      | [콘텐츠](/help/reporting/dimensions/content.md) | 차원 | `mediaReporting.sessionDetails.name` | 미디어: 컨텐츠 ID |
      | [콘텐츠 이름](/help/reporting/dimensions/content-name.md) | 차원 | `mediaReporting.sessionDetails.friendlyName` | 미디어: 비디오 이름 |
      | [콘텐츠 길이](/help/reporting/dimensions/content-length.md) | 차원 | `mediaReporting.sessionDetails.length` | 미디어: 비디오 길이 |
      | [표시](/help/reporting/dimensions/show.md) | 차원 | `mediaReporting.sessionDetails.show` | 미디어: 표시 |
      | [시즌](/help/reporting/dimensions/season.md) | 차원 | `mediaReporting.sessionDetails.season` | 미디어 : 시즌 |
      | [에피소드](/help/reporting/dimensions/episode.md) | 차원 | `mediaReporting.sessionDetails.episode` | 미디어: 에피소드 |
      | 이벤트 유형 | 차원 | `eventType` | 미디어: 이벤트 유형 |
      | [콘텐츠 체류 시간](/help/reporting/metrics/content-time-spent.md) | 지표 | `mediaReporting.sessionDetails.timePlayed` | 미디어: 컨텐츠 체류 시간 |
      | [미디어 체류 시간](/help/reporting/metrics/media-time-spent.md) | 지표 | `mediaReporting.sessionDetails.totalTimePlayed` | 미디어: 미디어 사용 시간 |
      | [총 일시 중단 기간](/help/reporting/metrics/total-pause-duration.md) | 지표 | `mediaReporting.sessionDetails.pauseTime` | 미디어: 총 일시 중단 기간 |
      | [시작 시간](/help/reporting/metrics/time-to-start.md) | 지표 | `mediaReporting.qoeDataDetails.timeToStart` | 미디어: 시작 시간 |
      | [총 버퍼 지속 시간](/help/reporting/metrics/total-buffer-duration.md) | 지표 | `mediaReporting.qoeDataDetails.bufferTime` | 미디어: 총 버퍼 지속 시간 |
      | 미디어 세션 서버 시간 초과 | 지표 | `mediaReporting.sessionDetails.secondsSinceLastCall` | 미디어: 마지막 통화 이후 지난 시간(초) |

      >[!IMPORTANT]
      >
      >스트리밍 미디어 패널이 작동하려면 이 테이블의 컨텍스트 레이블이 필요합니다. Customer Journey Analytics은 이 지표를 사용하여 **동시 뷰어** 및 **재생 소요 시간** 파생 지표([미디어 동시 뷰어](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) 및 [미디어 재생 소요 시간](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent) 패널에서 사용)를 자동으로 계산하고 [미디어 분당 평균 시청 시간](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel) 패널에서 보고 옵션을 채웁니다.

      이 시점에서 다른 [차원](/help/reporting/dimensions/overview.md) 또는 [지표](/help/reporting/metrics/overview.md)을(를) 데이터 보기에 추가할 수 있습니다. 각 페이지에는 해당 구성 요소에 대한 XDM 경로가 나열됩니다.

1. 변경 내용을 저장하려면 **[!UICONTROL 저장 후 계속]**→ **[!UICONTROL 저장 후 마침]**&#x200B;을 선택하십시오.

## Customer Journey Analytics에서 프로젝트 만들기 및 구성

1. Customer Journey Analytics의 **[!UICONTROL Workspace]** 탭의 **[!UICONTROL 프로젝트]** 영역에서 **[!UICONTROL 프로젝트 만들기]**&#x200B;를 선택합니다.

1. **[!UICONTROL 만들기]**→ **[!UICONTROL 빈 프로젝트]**&#x200B;을(를) 선택하십시오.

1. 새 프로젝트에서 이전에 만든 데이터 보기를 선택합니다.

   프로젝트에서 패널을 만들 때 데이터 보기에 추가한 구성 요소를 사용할 수 있습니다.

1. 왼쪽 레일에서 **패널** 아이콘을 선택한 다음 **[!UICONTROL 미디어 분당 평균 시청 시간]**, **[!UICONTROL 미디어 동시 뷰어]** 및 **[!UICONTROL 미디어 재생 소요 시간]** 패널에서 드래그합니다.

1. (조건부) 사용자 지정 메타데이터를 스키마에 추가한 경우 Customer Journey Analytics 안내서의 [지속성 구성 요소 설정](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)에 설명된 대로 사용자 지정 필드의 지속성을 설정하십시오.

1. [프로젝트 공유](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=ko)에 설명된 대로 프로젝트를 공유합니다.

   >[!NOTE]
   >
   >공유하려는 사용자를 사용할 수 없는 경우 사용자에게 Adobe Admin Console의 Customer Journey Analytics에 대한 사용자 및 관리자 액세스 권한이 있는지 확인하십시오.

## Customer Journey Analytics에서 사용 가능한 미디어 패널

Customer Journey Analytics의 Analysis Workspace에는 스트리밍 미디어 컬렉션 추가 기능을 사용하는 고객을 위한 3개의 전용 미디어 패널이 포함되어 있습니다. 이러한 패널은 가장 일반적인 스트리밍 미디어 보고 요구 사항에 대해 미리 빌드된 시각화를 제공합니다.

* **[미디어 분당 평균 시청 시간](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel)**: 모든 길이 또는 모든 장르의 프로그램에서 평균 콘텐츠 소비를 비교합니다. 특정 콘텐츠(기간 기반)와 사용자 지정 기간 모드를 모두 지원하며, 이후 기간 분류를 업데이트할 수 있습니다.
* **[미디어 동시 뷰어](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)**: 시간 경과에 따른 동시 뷰어를 분석하여 최대 동시 시청 및 시청 감소 지점을 식별합니다. 세그먼트, 차원 또는 날짜 범위별로 구성 가능한 세부 기간 및 시리즈 분류를 지원합니다.
* **[미디어 재생 소요 시간](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)**: 최대 및 저점 기간에 대한 세부 정보를 사용하여 시간 경과에 따른 재생 기간을 분석합니다. 구성 가능한 세부 기간 및 출력 형식(시간 또는 분)을 지원합니다.

>[!MORELIKETHIS]
>
>* [차원 개요](/help/reporting/dimensions/overview.md)
>* [지표 개요](/help/reporting/metrics/overview.md)
