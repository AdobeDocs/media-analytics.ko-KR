---
title: Streaming Media 지표 개요
description: Adobe Analytics 및 Customer Journey Analytics에서 스트리밍 미디어 지표를 계산하고 구성하는 방법에 대해 알아봅니다.
feature: Metrics
role: User, Admin
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 3%

---


# Streaming Media 지표 개요

Streaming Media Analytics의 지표는 미디어 백엔드에서 계산한 이벤트 기반 카운트 및 기간입니다. 미디어 플레이어는 세션 시작, 재생, ping 및 광고 시작과 같은 이벤트를 전송합니다. 미디어 백엔드는 이러한 이벤트를 처리하고 세션 닫기 호출에 대한 지표 값을 완료합니다.

## 지표 계산 방법

Streaming Media 지표는 다음과 같은 네 가지 기본 계산 패턴을 따릅니다.

* **이벤트 트리거 플래그**: 자격 있는 이벤트가 세션에 처음 도착할 때 설정합니다. 기본 콘텐츠에 대한 [`play`](/help/implementation/events/playback/play.md) 이벤트는 [[!UICONTROL 콘텐츠 시작]](content-starts.md) 플래그를 설정하고 [`adStart`](/help/implementation/events/ads/ad-start.md) 이벤트는 [[!UICONTROL 광고 시작]](ad-starts.md)을 설정합니다. 플래그는 이벤트별이 아니라 닫기 호출의 세션별로 한 번 보고됩니다.

* **누적 기간**: 특정 재생 상태가 활성 상태인 동안 ping 이벤트 사이의 간격을 합합니다. 기본 컨텐츠가 재생되는 동안 [[!UICONTROL 컨텐츠 체류 시간]](content-time-spent.md)이 누적되고, 광고가 재생되는 동안 [[!UICONTROL 광고 체류 시간]](ad-time-spent.md)이 누적됩니다. Adobe의 권장 ping 간격은 기본 컨텐츠의 경우 10초이고, 광고 중에는 1초이므로, 체류 시간 지표는 구현의 ping 간격만큼 세부적일 수만 있습니다.

* **이벤트 수**: 세션 내의 총 발생 횟수를 추적합니다. [[!UICONTROL 버퍼 이벤트]](buffer-events.md), [[!UICONTROL 비트율 변경]](bitrate-changes.md), [[!UICONTROL 오류 이벤트]](error-events.md) 및 [[!UICONTROL 이벤트 일시 중지]](pause-events.md)와 같은 품질 지표는 처음뿐만 아니라 모든 경우에 계산됩니다.

* **영향을 받은 스트림**: 세션 중 해당 이벤트가 횟수에 관계없이 언제든지 발생한 경우 세션 수준 플래그를 1로 설정합니다. 이 지표를 사용하여 도달 범위를 측정하고 이벤트 수 지표를 사용하여 심각도를 측정합니다. 예를 들어 [[!UICONTROL 버퍼가 영향을 받은 스트림]](buffer-impacted-streams.md)을 사용하여 모든 재생 세션에서 버퍼링의 영향을 받은 세션의 비율을 확인할 수 있습니다.

## 보고 시스템별 가용성

| 보고 시스템 | 지표 도착 방법 |
| --- | --- |
| Adobe Analytics | [컨텍스트 데이터 변수](https://experienceleague.adobe.com/ko/docs/analytics/implementation/vars/page-vars/contextdata)을 사용하여 채워집니다. 일부 지표는 이러한 컨텍스트 데이터 변수를 사용하여 솔루션 이벤트를 자동으로 채우는 반면, 다른 지표는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을 사용하여 사용자 지정 이벤트에 매핑해야 합니다. 값을 자동으로 채우는 지표에는 해당 [스트리밍 미디어 보고서 세트 설정](../../implementation/media-sdk/setup/media-reports-enable.md)이 먼저 활성화되어 있어야 합니다. |
| Customer Journey Analytics | 스트리밍 미디어 데이터를 포함하는 모든 데이터 집합에서 가져온 `xdm.mediaReporting.sessionDetails` 및 관련 노드의 XDM 필드. [데이터 보기 구성 요소 설정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview) 내에서 원하는 설정으로 각 지표를 만들어야 합니다. |
| 데이터 피드 | 지표가 `event_list` 및 `post_event_list` 열에 이벤트 ID로 나타납니다. 각 피드 파일에는 스트리밍 미디어 지표를 포함하여 모든 지표에 대한 조회가 포함된 `events.csv` 파일이 포함되어 있습니다. |

>[!MORELIKETHIS]
>
>* [차원 개요](../dimensions/overview.md): 스트리밍 미디어 차원 참조
>* [계산된 지표](/help/reporting/calculated-metrics.md): 위의 기본 지표에서 만들어진 비율 및 파생 지표
>* [매개 변수 매핑](/help/implementation/parameters-mapping.md): 전체 이벤트-열-XDM 참조
>* [이벤트 개요](/help/implementation/events/overview.md): 지표 계산을 유도하는 플레이어 이벤트
