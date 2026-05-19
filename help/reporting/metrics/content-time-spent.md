---
title: 콘텐츠 체류 시간
description: 세션당 활성 기본 컨텐츠 재생의 총 시간(초)을 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 6%

---


# 콘텐츠 체류 시간

**콘텐츠 체류 시간** 지표는 광고, 일시 중지, 버퍼링 및 정지를 제외하고 세션당 활성 기본 콘텐츠 재생의 총 시간(초)을 보고합니다. 콘텐츠 보기를 위한 참여 지표로 사용합니다. 광고를 포함하여 사용한 시간은 [미디어 사용 시간](media-time-spent.md)을 참조하세요.

## 이 지표의 계산 방법

미디어 백엔드는 플레이어가 기본 콘텐츠의 `play` 상태에 있는 동안 이벤트 간에 경과된 월 클럭 시간을 합산합니다. 광고, 일시 중지, 버퍼 이벤트 및 중지 중의 시간은 제외됩니다. 활성 재생 시간만 계산되므로 뷰어가 뒤로 이동하고 세그먼트를 다시 볼 때 지표는 [콘텐츠 길이](/help/reporting/dimensions/content-length.md)를 초과할 수 있습니다. 지정된 세그먼트를 통과하는 각 과정은 추가 재생 시간을 누적하며, 사용자가 세션에서 콘텐츠를 소비하고 되감는 동안 발생할 수 있습니다. 지표는 닫기 호출에 보고됩니다. 이 값은 Analysis Workspace에서 `HH:MM:SS`(으)로 표시되고, 데이터 피드, Data Warehouse 및 보고 API에서는 초 단위로 표시됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.timePlayed`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.timePlayed` |
