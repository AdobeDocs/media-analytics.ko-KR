---
title: 미디어 시작
description: 프리롤 광고 또는 버퍼링으로 종료된 세션을 포함하여 시작된 모든 미디어 세션을 계산합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# 미디어 시작

**미디어 시작** 지표는 시작된 모든 미디어 세션을 계산합니다. 프리롤 광고, 버퍼링 중에 또는 기본 콘텐츠가 재생되기 전에 뷰어가 드롭아웃되더라도 백엔드가 `media.sessionStart` 이벤트를 받으면 즉시 증가합니다. 미디어 보고를 위한 가장 광범위한 funnel 맨 위 지표로 사용하십시오. 광고 및 버퍼 드롭오프를 측정하려면 [콘텐츠 시작](content-starts.md)과(와) 연결하십시오.

## 이 지표의 계산 방법

`media.sessionStart` 이벤트가 수신되면 미디어 백엔드가 `mediaReporting.sessionDetails.isViewed = true`을(를) 설정합니다. 보고된 지표는 세션당 `1`입니다. 종료 호출이 아닌 시작 호출 시 미디어 시작이 보고됩니다. 세션 닫기를 기다리지 않는 유일한 1단계 지표입니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.view`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
