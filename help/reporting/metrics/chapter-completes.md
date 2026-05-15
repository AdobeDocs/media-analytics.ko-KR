---
title: 챕터 완료
description: 완료까지 재생된 모든 챕터를 계산합니다.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 12%

---


# 챕터 완료

**챕터 완료** 지표는 완료 시까지 재생된 모든 챕터를 계산합니다. [챕터 시작](chapter-starts.md)과(와) 연결하여 챕터 완료율을 계산합니다.

## 이 지표의 계산 방법

[챕터 완료](/help/implementation/events/chapters/chapter-complete.md) 이벤트가 수신되면 미디어 백엔드가 `mediaReporting.chapterDetails.isCompleted = true`을(를) 설정합니다. 지표는 챕터 닫기 호출에 보고됩니다. 건너뛴 챕터 또는 포기한 중간 플레이는 완료로 계산되지 않습니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 챕터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.chapter.complete`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.chapter.complete` |
