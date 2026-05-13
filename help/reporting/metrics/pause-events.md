---
title: 이벤트 일시 중지
description: 세션 중에 발생한 개별 일시 중지를 모두 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 10%

---


# 이벤트 일시 중지

**일시 중지 이벤트** 지표는 동일한 세션 내에서 여러 번 일시 중지를 포함하여 세션 중에 받은 모든 개별 `media.pauseStart` 이벤트를 계산합니다. 평균 일시 중지 길이를 파생하려면 [총 일시 중지 기간](total-pause-duration.md)을 사용하고, 최소 한 번 이상 일시 중지된 세션을 계산하려면 [일시 중지된 영향을 받은 스트림](paused-impacted-streams.md)을 사용합니다.

## 이 지표의 계산 방법

미디어 백엔드는 `media.pauseStart` 이벤트마다 `mediaReporting.sessionDetails.pauseCount`을(를) 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.pauseCount`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
