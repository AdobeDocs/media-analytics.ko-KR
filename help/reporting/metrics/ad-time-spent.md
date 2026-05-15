---
title: 광고 체류 시간
description: 세션당 활성 광고 재생의 총 시간(초)을 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 9%

---


# 광고 체류 시간

**광고 체류 시간** 지표는 일시 중지, 버퍼링 및 정지를 제외하고 세션당 활성 광고 재생의 총 시간(초)을 보고합니다. 광고 로드를 콘텐츠 참여와 비교하려면 [콘텐츠 체류 시간](/help/reporting/metrics/content-time-spent.md)과(와) 페어링하십시오.

## 이 지표의 계산 방법

미디어 백엔드는 플레이어가 광고에서 `play` 상태에 있는 동안 이벤트 간에 경과된 월 클럭 시간을 합산합니다. 일시 중지 및 버퍼링 중의 시간은 제외됩니다. 지표는 광고 닫기 호출에 보고됩니다. 이 값은 Analysis Workspace에서 `HH:MM:SS`(으)로 표시되고, 데이터 피드, Data Warehouse 및 보고 API에서는 초 단위로 표시됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 광고]](/help/reporting/media-reports-enable.md)를 사용하도록 설정한 경우 컨텍스트 데이터 `a.media.ad.timePlayed`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.ad.timePlayed` |
