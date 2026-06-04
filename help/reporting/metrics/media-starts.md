---
title: 미디어 시작
description: 프리롤 광고 또는 버퍼링으로 종료된 세션을 포함하여 시작된 모든 미디어 세션을 계산합니다.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 6%

---


# 미디어 시작

**미디어 시작** 지표는 시작된 모든 미디어 세션을 계산합니다. 프리롤 광고, 버퍼링 중에 또는 기본 콘텐츠가 재생되기 전에 뷰어가 드롭아웃되더라도 백엔드가 [세션 시작](/help/implementation/events/session/session-start.md) 이벤트를 받는 즉시 증가합니다. 미디어 보고를 위한 가장 광범위한 funnel 맨 위 지표로 사용하십시오. 광고 및 버퍼 드롭오프를 측정하려면 [콘텐츠 시작](content-starts.md)과(와) 연결하십시오.

## 이 지표의 계산 방법

[세션 시작](/help/implementation/events/session/session-start.md) 이벤트가 수신되면 미디어 백엔드가 이 플래그를 설정합니다. 보고된 지표는 세션당 `1`입니다. 미디어 시작은 닫기 호출이 아닌 시작 호출 시 보고되며 세션 닫기를 기다리지 않는 유일한 지표입니다. [콘텐츠 시작](/help/reporting/metrics/content-starts.md), [콘텐츠 체류 시간](/help/reporting/metrics/content-time-spent.md) 및 [진행률 마커](/help/reporting/metrics/progress-markers.md)를 포함한 다른 모든 미디어 지표는 닫기 호출에 보고되며 재생 중에 실시간으로 사용할 수 없습니다. [광고 시작](/help/reporting/metrics/ad-starts.md)은(는) 종료 시간이 아닌 트리거 이벤트에 대해 보고된 추가적인 지표입니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.view`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.view` |
