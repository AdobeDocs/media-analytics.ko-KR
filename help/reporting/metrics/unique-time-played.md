---
title: 재생된 고유 시간
description: 세션 중에 본 고유 콘텐츠(초)를 보고하여 검색 후 재생을 중복 제거합니다.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# 재생된 고유 시간

**재생된 고유 시간** 지표는 세션 중에 표시되는 개별 콘텐츠의 시간(초)을 보고하여 검색 되돌림을 통해 재생된 세그먼트의 중복을 제거합니다. [콘텐츠 체류 시간](content-time-spent.md)과(와) 비교하면, 뷰어가 동일한 세션 내에서 동일한 콘텐츠의 일부를 다시 볼 때 고유 재생 시간이 더 짧습니다.

## 이 지표의 계산 방법

미디어 백엔드는 세션 중에 열람된 플레이헤드 간격을 추적하고 해당 합계를 합산합니다. 동일한 5초 세그먼트를 두 번 재생해도 5초로 계산됩니다. 지표는 닫기 호출에 보고됩니다. 이 값은 Analysis Workspace에서 `HH:MM:SS`(으)로 표시되고, 데이터 피드, Data Warehouse 및 보고 API에서는 초 단위로 표시됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.uniqueTimePlayed`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.uniqueTimePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.uniqueTimePlayed` |
