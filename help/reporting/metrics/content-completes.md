---
title: 컨텐츠 완료
description: 플레이헤드가 콘텐츠 끝에 도달한 세션을 카운트합니다.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 10%
---

# 컨텐츠 완료

**콘텐츠 완료** 지표는 플레이헤드가 콘텐츠 끝에 도달한 세션을 계산합니다. 완료율을 계산하려면 [콘텐츠 시작](content-starts.md)과(와) 짝을 이루고, 전체 보기 속도를 계산하려면 [미디어 시작](media-starts.md)과(와) 짝을 지으세요.

## 이 지표의 계산 방법

[세션 완료](/help/implementation/events/session/session-complete.md) 이벤트가 수신되면 미디어 백엔드가 이 플래그를 설정합니다. 지표는 닫기 호출에 보고됩니다. 명시적 `sessionComplete` 없이 시간 초과된 세션은 완료로 계산되지 않습니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.complete`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.complete` |
