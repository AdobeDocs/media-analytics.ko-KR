---
title: 시작 전 드롭
description: 기본 컨텐츠가 렌더링되기 전에 뷰어가 종료되는 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 8%

---


# 시작 전 드롭

**시작 전 드롭** 지표는 뷰어가 주 콘텐츠를 렌더링하기 전에 종료되는 세션을 계산합니다. 이 지표는 광고 동작과 관계없이 사전 콘텐츠 포기에 플래그를 지정하므로 순수 사전 콘텐츠 드롭오프의 가장 좋은 방법입니다. [미디어 시작](/help/reporting/metrics/media-starts.md) 및 [콘텐츠 시작](/help/reporting/metrics/content-starts.md)과(와) 연결하여 콘텐츠 프레임을 만들지 않은 세션의 공유를 계산합니다.

## 이 지표의 계산 방법

미디어 백엔드는 기본 콘텐츠에 `media.play` 이벤트를 생성하지 않고 종료되는 세션에 대해 `mediaReporting.qoeDataDetails.isDroppedBeforeStart = true`을(를) 설정합니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.dropBeforeStart`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
