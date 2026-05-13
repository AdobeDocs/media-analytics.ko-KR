---
title: 총 버퍼 지속 시간(지표)
description: 세션 간 합계 및 평균에 대한 누적 버퍼 시간을 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# 총 버퍼 지속 시간(지표)

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**총 버퍼 지속 시간**&#x200B;지표를 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.bufferTime` 컨텍스트 데이터 변수에서 쌍을 이루는 [총 버퍼 지속 시간(차원)](/help/reporting/dimensions/total-buffer-duration.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `mediaReporting.qoeDataDetails.bufferTime` 필드를 노출합니다.*

>[!ENDSHADEBOX]

**총 버퍼 지속 시간** 지표는 합계, 평균 및 백분위수 롤업에 적합한 세션 간 누적 버퍼 시간을 보고합니다. 이 지표를 사용하여 고객이 보고서 기간에 버퍼에서 대기하는 데 걸린 총 시간을 계산합니다.

## 이 지표의 계산 방법

미디어 백엔드는 모든 버퍼 간격(`media.bufferStart`부터 다음 상태 변경까지)의 기간을 합합니다. 지표는 닫기 호출에 보고됩니다. Analysis Workspace은 값을 `HH:MM:SS`(으)로 표시합니다. 데이터 피드, Data Warehouse 및 보고 API는 값(초)을 표시합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.bufferTime`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
