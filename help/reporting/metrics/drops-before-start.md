---
title: 시작 전 드롭
description: 기본 컨텐츠가 렌더링되기 전에 뷰어가 종료되는 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 7%

---


# 시작 전 드롭

**시작 전 드롭** 지표는 뷰어가 주 콘텐츠를 렌더링하기 전에 종료되는 세션을 계산합니다. 이 지표는 광고 동작과 관계없이 사전 콘텐츠 포기에 플래그를 지정하므로 순수 사전 콘텐츠 드롭오프의 가장 좋은 방법입니다. [미디어 시작](/help/reporting/metrics/media-starts.md) 및 [콘텐츠 시작](/help/reporting/metrics/content-starts.md)과(와) 연결하여 콘텐츠 프레임을 만들지 않은 세션의 공유를 계산합니다.

## 이 지표의 계산 방법

미디어 백엔드는 기본 콘텐츠에서 [play](/help/implementation/events/playback/play.md) 이벤트를 생성하지 않고 종료되는 세션에 대해 이 플래그를 설정합니다. 지표는 닫기 호출에 보고됩니다. 일반적인 시나리오에는 프리롤 광고 동안 뷰어가 종료되거나, 플레이어가 초기 버퍼 단계에서 무기한 중단되거나, 첫 번째 기본 컨텐츠 재생 이벤트 전에 오류가 발생하는 경우가 있습니다. 이 모든 경우 세션은 [미디어 시작](/help/reporting/metrics/media-starts.md)을 기록하지만 [콘텐츠 시작](/help/reporting/metrics/content-starts.md)은 기록하지 않으며 [진행률 마커](/help/reporting/metrics/progress-markers.md)는 기록되지 않습니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.dropBeforeStart`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.qoe.dropBeforeStart` |
