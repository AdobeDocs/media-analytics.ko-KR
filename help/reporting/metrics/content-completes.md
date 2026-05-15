---
title: 컨텐츠 완료
description: 플레이헤드가 콘텐츠 끝에 도달한 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 10%

---


# 컨텐츠 완료

**콘텐츠 완료** 지표는 플레이헤드가 콘텐츠 끝에 도달한 세션을 계산합니다. 완료율을 계산하려면 [콘텐츠 시작](content-starts.md)과(와) 짝을 이루고, 전체 보기 속도를 계산하려면 [미디어 시작](media-starts.md)과(와) 짝을 지으세요.

## 이 지표의 계산 방법

[세션 완료](/help/implementation/events/session/session-complete.md) 이벤트가 수신되면 미디어 백엔드가 `mediaReporting.sessionDetails.isCompleted = true`을(를) 설정합니다. 지표는 닫기 호출에 보고됩니다. 명시적 `sessionComplete` 없이 시간 초과된 세션은 완료로 계산되지 않습니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.complete`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.complete` |
