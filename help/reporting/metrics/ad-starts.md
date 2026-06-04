---
title: 광고 시작
description: 세션 중에 재생되기 시작한 모든 광고를 계산합니다.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 11%

---


# 광고 시작

**광고 시작** 지표는 세션 중에 재생되기 시작한 모든 광고를 계산합니다. 광고 완료율을 계산하려면 [광고 완료](ad-completes.md)와 쌍을 이루고, 동등한 세션 수준 롤업에 대해서는 [광고 수](/help/reporting/metrics/ad-count.md)와 쌍을 이루십시오.

## 이 지표의 계산 방법

[광고 시작](/help/implementation/events/ads/ad-start.md) 이벤트가 수신되면 미디어 백엔드가 이 플래그를 설정합니다. 지표는 광고 시작 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 광고]](/help/reporting/setup/analytics-reporting.md)를 사용하도록 설정한 경우 컨텍스트 데이터 `a.media.ad.view`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.ad.view` |
