---
title: 총 일시 중단 기간
description: 세션 중 뷰어가 일시 중지된 상태로 보낸 누적 시간(초)을 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 8%

---


# 총 일시 중단 기간

**총 일시 중지 기간** 지표는 세션 중에 뷰어가 일시 중지된 총 체류 시간(초)을 보고합니다. 지표는 각 `media.pauseStart`과(와) 후속 `media.play` 사이의 모든 간격의 합계입니다. 여러 일시 정지가 함께 추가됩니다. [일시 중지 이벤트](pause-events.md)와(과) 연결하여 평균 일시 중지 길이를 파생합니다.

## 이 지표의 계산 방법

미디어 백엔드는 모든 `media.pauseStart`과(와) 일치하는 `media.play` 이벤트 사이의 경과된 월-시계 시간을 합산합니다. 지표는 닫기 호출에 보고됩니다. 값은 Analysis Workspace에서 `HH:MM:SS`(으)로 표시되고 다른 곳에서는 초 단위로 표시됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.pauseTime`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
