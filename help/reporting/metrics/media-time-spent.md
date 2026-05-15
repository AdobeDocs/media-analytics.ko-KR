---
title: 미디어 체류 시간
description: 광고를 포함하여 세션당 활성 재생의 총 시간(초)을 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 8%

---


# 미디어 체류 시간

**미디어 체류 시간** 지표는 기본 콘텐츠와 광고를 모두 포함하지만 일시 중지, 버퍼링 및 정지를 제외한 세션당 활성 재생의 총 시간(초)을 보고합니다. 시청자가 플레이어에 적극적으로 참여한 총 시간을 측정하는 데 사용합니다. 기본 콘텐츠의 경우 [콘텐츠 체류 시간](content-time-spent.md)을 사용하십시오.

## 이 지표의 계산 방법

미디어 백엔드는 플레이어가 기본 콘텐츠 또는 광고에서 `play` 상태에 있는 동안 이벤트 간에 경과된 월 클럭 시간을 합산합니다. 일시 중지, 버퍼 이벤트 및 중지 중의 시간은 제외됩니다. 지표는 닫기 호출에 보고됩니다. 이 값은 Analysis Workspace에서 `HH:MM:SS`(으)로 표시되고, 데이터 피드, Data Warehouse 및 보고 API에서는 초 단위로 표시됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.totalTimePlayed`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.totalTimePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.totalTimePlayed` |
