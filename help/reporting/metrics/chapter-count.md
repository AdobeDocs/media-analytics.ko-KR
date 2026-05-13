---
title: 챕터 수
description: 세션 중에 시작된 챕터의 수를 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 7%

---


# 챕터 수

**챕터 수** 지표는 세션 중에 시작된 챕터의 수를 보고합니다. 이를 사용하여 콘텐츠 간 챕터 소비를 비교합니다. 챕터 차원(챕터 이름, 위치)에 의해 피벗된 챕터 시작 횟수의 경우 챕터 변수 범주가 활성화되면 사용할 수 있는 챕터 시작 지표를 사용합니다.

## 이 지표의 계산 방법

미디어 백엔드는 세션 중에 받은 `media.chapterStart` 이벤트마다 `mediaReporting.sessionDetails.chapterCount`을(를) 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | `a.media.chapterCount`을(를) 사용자 지정 이벤트에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/ko/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.chapterCount`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`(처리 규칙이 `a.media.chapterCount`을(를) 매핑하는 사용자 지정 이벤트. [`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
