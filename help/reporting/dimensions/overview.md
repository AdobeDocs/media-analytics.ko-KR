---
title: 스트리밍 미디어 차원 개요
description: Adobe Analytics 및 Customer Journey Analytics에서 스트리밍 미디어 차원을 채우고 구성하는 방법에 대해 알아봅니다.
feature: Dimensions
role: User, Admin
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---


# 스트리밍 미디어 차원 개요

Streaming Media Analytics의 차원을 사용하면 컨텐츠 이름, 스트림 유형, 광고 이름 및 수십 개의 다른 속성으로 지표를 분할하고 필터링할 수 있습니다. 대부분은 세션 시작 시 플레이어에 의해 설정되고 세션 닫기로 전달됩니다.

## 차원 채우기 방법

Streaming Media 차원은 다음 세 가지 주요 모집단 패턴을 따릅니다.

* **미디어 플레이어에서 제공**: 대부분의 차원에 대한 소스입니다. 플레이어가 [세션 시작](/help/implementation/events/session/session-start.md) 호출에서 이러한 값을 보내고 미디어 백엔드가 해당 값을 세션의 모든 후속 이벤트에 연결합니다. 세션 시작 시 플레이어가 보내는 것은 보고서에 표시되는 내용입니다. 예로는 [[!UICONTROL 스트림 형식]](/help/reporting/dimensions/stream-type.md), [[!UICONTROL 콘텐츠 이름]](/help/reporting/dimensions/content-name.md) 및 [[!UICONTROL 콘텐츠 길이]](/help/reporting/dimensions/content-length.md)가 있습니다.

* **파생 값**: 미디어 백 엔드가 플레이어에서 제공한 값을 읽는 대신 누적된 재생 상태에서 계산하는 차원입니다. [[!UICONTROL 콘텐츠 세그먼트]](/help/reporting/dimensions/content-segment.md)은(는) 재생 과정에서 재생 헤드 위치에서 계산됩니다. [[!UICONTROL 미디어 경로]](/help/reporting/dimensions/media-path.md)은(는) 세션에서 콘텐츠와 광고 상태 사이의 전환을 추적합니다. 플레이어에서 이러한 차원을 재정의할 수 없습니다.

* **분류**: 선택 사항입니다. 별도의 차원을 채우는 대신 [분류 세트](https://experienceleague.adobe.com/ko/docs/analytics/components/classifications/sets/overview)&#x200B;(Adobe Analytics) 또는 [조회 데이터 세트](https://experienceleague.adobe.com/en/docs/analytics-platform/using/compare-aa-cja/upgrade-to-cja/create-datasets/cja-upgrade-dataset-lookup)&#x200B;(Customer Journey Analytics)를 사용하여 분류 데이터를 유지 관리할 수 있습니다.

## 보고 시스템별 가용성

| 보고 시스템 | 차원 도착 방법 |
| --- | --- |
| Adobe Analytics | [컨텍스트 데이터 변수](https://experienceleague.adobe.com/ko/docs/analytics/implementation/vars/page-vars/contextdata)을 사용하여 채워집니다. 일부 차원은 이러한 컨텍스트 데이터 변수를 사용하여 자동으로 차원을 채우지만, 다른 차원은 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을 사용하여 채워야 합니다. 값을 자동으로 채우는 차원에는 먼저 해당 [스트리밍 미디어 보고서 세트 설정](../../implementation/media-sdk/setup/media-reports-enable.md)이 활성화되어 있어야 합니다. |
| Customer Journey Analytics | 스트리밍 미디어 데이터를 포함하는 모든 데이터 집합에서 가져온 `xdm.mediaReporting.sessionDetails`의 XDM 필드. [데이터 보기 구성 요소 설정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview) 내에서 원하는 설정으로 각 차원을 만들어야 합니다. |
| 데이터 피드 | 자동으로 채워진 차원에는 고유한 데이터 피드 열 이름(`videostreamtype`, `videoname` 또는 `videolength`)이 있습니다. 처리 규칙이 필요한 차원에서는 `evar` 열 이름을 사용합니다. |
| Audience Manager | Adobe Analytics에서 전달된 컨텍스트 데이터. Analytics에서 Audience Manager으로 서버측 전달이 구성된 경우에만 사용할 수 있습니다. |

>[!MORELIKETHIS]
>
>* [이벤트 개요](/help/implementation/events/overview.md): 차원을 채우는 플레이어 이벤트
>* [변수 개요](/help/implementation/variables/overview.md): 이벤트가 Adobe으로 전달하는 데이터
>* [지표 개요](/help/reporting/metrics/overview.md): 변수가 채우는 보고 지표입니다
